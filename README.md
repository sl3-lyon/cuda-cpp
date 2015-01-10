# cuda-cpp
Surcouche C++ de CUDA C

**Doc**

Kernels :
__global__ => Appelé par le CPU, exécuté par le GPU
__device__ => Appelé et exécuté par le GPU
__host__   => Appelé et exécuté par le CPU (mode par défaut)

__global__
- Exécuté sur le périphérique,
- Appelable de l'hôte.
- Pas de récursion possible,
- Pas de variables statiques,
- Pas de liste de paramètres variable.
- On ne peut demander leur adresse mémoire,
- Incompatible avec __device__,
- Ne peut rien retourner,
- À l'exécution, on doit préciser la configuration,
- Appel asynchrone (le kernel retourne avant d'avoir effectué les calculs),
- Paramètres stockés dans la mémoire partagée, limités à 256 octets,
- Dure aussi longtemps que le kernel.

__device__
- Exécuté sur le périphérique,
- Appelable du périphérique.
- Pas de récursion possible,
- Pas de variables statiques,
- Pas de liste de paramètres variable.
- On ne peut demander leur adresse mémoire,
- Incompatible avec __global__,
- Dure aussi longtemps que l'application.

__host__
- Exécuté sur l'hôte,
- Appelable de l'hôte.
- Appliqué par défaut.
- Compatible avec __device__ (dans ce cas, le kernel pourra être exécuté sur l'hôte et sur le périphérique),
- Incompatible avec __global__,
- Dure aussi longtemps que le kernel.

Appel de kernel :
kernel<<<blocks, threadsParBloc>>>(arguments);

Grille contient blocs, exécutant threads :
|- Bloc -------------------------------|
|                                      |
|  ----------  ----------  ----------  |
|  | Thread |  | Thread |  | Thread |  |
|  ----------  ----------  ----------  |
|                                      |
|  ----------  ----------  ----------  |
|  | Thread |  | Thread |  | Thread |  |
|  ----------  ----------  ----------  |
|                                      |
|--------------------------------------|

Chaque kernel dispose de variables implicites en lecture seule, toutes de type dim3 (struct avec x, y, z) :
- blockIdx : index du bloc dans la grille,
- threadIdx : index du thread dans le bloc,
- blockDim : nombre de threads par bloc (valeur de threadsParBloc du paramétrage du kernel).
