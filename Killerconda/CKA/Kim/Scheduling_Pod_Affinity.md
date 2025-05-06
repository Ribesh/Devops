# Introduction (Scheduling Pod Affinity)

**Inter-pod affinity** and **anti-affinity** in Kubernetes are scheduling mechanisms that control *how pods are placed relative to other pods across nodes* in a cluster.
-   These features allow you to define rules to influence whether pods should be **co-located (affinity)** or **spread apart (anti-affinity)** based on ***labels***, enhancing workload distribution, high availability, and resource optimization.

-   They *extend the basic node-level affinity rules* by considering **existing pod labels**, **rather than node labels**.

## 1.   Overview
```Kubernetes schedulers``` decide where to place pods based on *resource availability, constraints, and user-defined policies*.

```Affinity``` and ```Anti-affinity``` rules extend this by allowing you to specify preferences or requirements for **pod placement relative to other pods**.

### A.  Inter-pod Affinity:
Specifies that a pod should be scheduled on a node (or near nodes) where certain other pods are already running, **based on labels.**
-   This is useful when pods need to be co-located for performance reasons (e.g., low-latency communication) or to share resources.

### B. Inter-pod Anti-Affinity
Specifies that a **pod should not be scheduled** on a node (or near nodes) **where certain other pods are running.**
-   This is useful for spreading pods across nodes to improve fault tolerance, load balancing, or to avoid resource contention.


#### Important
 Both mechanisms rely on ```labels``` and ```selectors``` to identify target pods and are defined in the pod’s specification under the affinity field. 
 -  They work in conjunction with ```Kubernetes’ scheduler``` to make placement decisions.

 ## 2. Key Concepts
 ### A. Labels and Selectors
-   Pods are identified using **labels** (key-value pairs) defined in their *metadata*.
-   Affinity/anti-affinity rules use **label selectors** to match pods that the rule applies to.
-   Example: A pod with label ```app=frontend``` can have an affinity rule to be scheduled near pods with ```app=backend```.


### B. Topology Domains
-   Affinity and anti-affinity rules are applied within a **topology domain**, which defines the scope of the rule (e.g., a node, rack, zone, or region).

-   The ```topologyKey``` field in the affinity rule specifies the node label that defines the topology. Common topologyKey values include:

    -   ```kubernetes.io/hostname```: Refers to a specific node.
    -   ```topology.kubernetes.io/zone```: Refers to a cloud provider’s availability zone.
    -   ```topology.kubernetes.io/region```: Refers to a cloud provider’s region.


### C. Hard vs. Soft Requirements
1.  **Hard Requirements** (```requiredDuringSchedulingIgnoredDuringExecution```):
    -    The scheduler **must satisfy** the affinity/anti-affinity rule for the pod to be scheduled 
    -   If no node satisfies the rule, **the pod remains unscheduled (pending).**
    -   Use for strict placement requirements.

2.  **Soft Requirements** (```preferredDuringSchedulingIgnoredDuringExecution```):
    -    The scheduler **tries to satisfy** the rule but **will schedule the pod even if the rule cannot be met.**
    -   A weight (1–100) is assigned to prioritize the rule among other preferences.
    -   Use for flexible placement preferences.

### D. IgnoredDuringExecution
-   The ```IgnoredDuringExecution``` part of the rule names means that **once a pod is scheduled, Kubernetes does not re-evaluate** affinity/anti-affinity rules if the cluster state changes (e.g., if other pods are added or removed).
-   To enforce ongoing affinity, you’d need custom controllers or manual intervention.

## 3. Configuration
Affinity and anti-affinity rules are defined in the affinity section of a pod’s specification (or a deployment, statefulset, etc.). Below are examples of each.

### Affinity Example
```bash
apiVersion: v1
kind: Pod
metadata:
  name: frontend-pod
spec:
  affinity:
    podAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
      - labelSelector:
          matchLabels:
            app: backend
        topologyKey: topology.kubernetes.io/zone
  containers:
  - name: frontend
    image: nginx
```

#### Explanation:
-   **podAffinity**: Specifies an affinity rule.
-   **requiredDuringSchedulingIgnoredDuringExecution**: Hard requirement.
-   **labelSelector**: Matches pods with app=backend.
-   **topologyKey**: topology.kubernetes.io/zone: Pods must be in the same zone.

### Anti-Affinity Example
Prevent a pod from being scheduled on a node with pods labeled ```app=database```:

```bash
apiVersion: v1
kind: Pod
metadata:
  name: app-pod
spec:
  affinity:
    podAntiAffinity:
      preferredDuringSchedulingIgnoredDuringExecution:
      - weight: 100
        podAffinityTerm:
          labelSelector:
            matchLabels:
              app: database
          topologyKey: kubernetes.io/hostname
  containers:
  - name: app
    image: nginx
```


#### Explanation:

-   **podAntiAffinity**: Specifies an anti-affinity rule.
-   **preferredDuringSchedulingIgnoredDuringExecution:** Soft requirement.
-   **weight: 100:** High priority for this rule.
-   **labelSelector:** Matches pods with app=database.
-   **topologyKey:** kubernetes.io/hostname: Avoids nodes with matching pods.


### Combining Rules
You can combine affinity and anti-affinity rules in the same pod spec. For example, you might want a pod to be near ```app=backend``` pods but avoid nodes with ```app=database``` pods.

```bash
apiVersion: v1
kind: Pod
metadata:
  name: complex-pod
spec:
  affinity:
    podAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
      - labelSelector:
          matchLabels:
            app: backend
        topologyKey: topology.kubernetes.io/zone
    podAntiAffinity:
      preferredDuringSchedulingIgnoredDuringExecution:
      - weight: 80
        podAffinityTerm:
          labelSelector:
            matchLabels:
              app: database
          topologyKey: kubernetes.io/hostname
  containers:
  - name: app
    image: nginx
```

### Combining with Node Affinity
```bash
apiVersion: v1
kind: Pod
metadata:
  name: combined-pod
spec:
  affinity:
    nodeAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
        nodeSelectorTerms:
        - matchExpressions:
          - key: disktype
            operator: In
            values:
            - ssd
    podAntiAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
      - labelSelector:
          matchLabels:
            app: database
        topologyKey: kubernetes.io/hostname
  containers:
  - name: app
    image: nginx
```