# minikube/kind/k3d comparsion

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
