# minikube/kind/k3d comparsion

# minikube
minikube is the Kubernetes community’s OG tool for quickly setting up Kubernetes locally, a first love for many Kubernetes novices. Initially, it simulated multi-node clusters via VMs on your local machine, offering a high-fidelity emulation of real-world scenarios, down to the OS and kernel module level. The downside? It’s a resource hog, and if your virtualization environment doesn’t support nested virtualization, you’re out of luck, not to mention it’s slow to start. Recently, the community introduced a Docker Driver to mitigate these issues, though at the cost of losing some VM-level emulation capabilities. On the bright side, minikube comes with a plethora of add-ons, like dashboards and nginx-ingress, for easy community component installation.

# kind
kind is a more recent favorite for local Kubernetes deployment, using Docker containers to simulate nodes and focusing purely on Kubernetes standard deployments, with community components requiring manual installation. It’s the go-to for Kubernetes’ own CI processes. The upside? Quick starts and a familiar environment for Docker veterans. The downside? Container simulation lacks OS-level isolation, sharing the host’s kernel, which can complicate OS-specific testing. I once had a kernel module test fail because the host’s netfilter tweaks caused havoc in a kind-managed cluster.

# k3d
k3d, a featherweight in local Kubernetes deployment, shares a similar approach to kind but opts for deploying a lightweight k3s instead of standard Kubernetes. This means it inherits k3s’s pros and cons, boasting incredibly fast setup times—don’t worry about correctness; just marvel at the speed. The trade-offs include a super-slimmed-down OS (sans glibc), complicating certain OS-level operations, and a unique installation approach that might puzzle those accustomed to kubeadm’s standard deployment features.


|  | minikube | kind | K3d |
|---------|----------|------|-----|
| runtime | VM | container | native |
| multi node cluster | + | + | + |
| single node cluster | + | + | + |
| arch support | x86, ARM64, ARMv7, ppc64 | AMD64, ARM64 | x86_64, AMD64, ARMv7, ARM64 |
| container runtimes | Docker, containerd, CRI-O | Docker, CRI-O | Docker, containerd |
| min cpu req | 2+ | 2+ | 1+ |
| min memory req | 2gb+ | 4gb+ | 512mb+ |
| root | no | no | yes |


# conclusion. a few notes here
Minikube is the easiest to use but it is not suitable for production.
For performance-constraint environments, k3d is easy to use the lightweight Kubernetes implementation. If speed if your only concern, k3d is the one.
KinD will need a resource. It offers a balanced compromise between performance and compatibility instead.


# URLs and materials used:
https://oilbeater.com/en/2024/02/22/minikube-vs-kind-vs-k3d/
https://alperenbayramoglu2.medium.com/simple-comparison-of-lightweight-k8s-implementations-7c07c4e6e95f
https://minikube.sigs.k8s.io/docs/benchmarks/timetok8s/v1.32.0/
