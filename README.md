# SEQUENCE

```mermaid
flowchart TD;
A[.SRCINFO]
A1[Build Files]
B[AUR Web Backend]
B1(Git Repo)
C[Makepkg or AUR Helper]
D[Stable PKGBUILD]
E[Source Files]
F[SHA256SUM]
G[Prepare]
H[BUILD]
I[Make]
J[Package For Arch]
K{{*.pkg.tar.zst}}
L[GPG/PGP]
M[\Install/]
N[/out\]
O{Release}

subgraph Clone
        subgraph  
        B1;
        end
end
B1--Build Files---C;

subgraph Backend
        subgraph  
                A--Metadata---B;
                A1---A;
                A1---B;
        end
end

subgraph Local
        subgraph  
                B--Metadata-->C;
                B--Build Files-->C;
                C--Start-->D;
                D--Download-->E;
                E--Verify Sources-->F;
                F--Verified-->G;
                G--Conf CMAKE & Apply Patch-->H;
                H--Flags-->I;
                I--BIN-->J;
                J--OUT-->K;
                K--Unsigned-->M;
                K--Sign-->L;
                L--Signed-->N
                N --*.pkg.tar.zst*--> O
        end
end
```
