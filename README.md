# Owl - An OCaml Math Library
Owl is an OCaml math library. It supports both dense and sparse matrix operations, linear algebra, regressions, and many advanced mathematical and statistical functions (such as Markov chain Monte Carlo methods).

## Installation

Installation is rather trivial. First, you need to clone the repository.

```bash
git clone git@github.com:ryanrhymes/owl.git
```

Then you need to install all the dependencies. Owl depends on gsl, ctypes, plplot, and several other modules. Check the `_oasis` file in the `owl` folder to find out the complete list of required modules.

Next, you can compile and install the module with the following command.

```bash
make oasis
make && make install
```

If you want `utop` to automatically load Owl for you, you can also edit `.ocamlinit` file in your home folder by adding the following lines.

```bash
#require "Owl"
#require "ctypes"
#require "ctypes.foreign"
```

Owl is well integrated with `utop`. Now you can start `utop` and continue this tutorial to do some experiments.


## Create Matrices

To start, we can use `Dense.uniform_int` to create a 5x5 random dense matrix.

```ocaml
let x = Dense.uniform_int 5 5;;
```

You should see the following output in `utop`.

```bash
   C0 C1 C2 C3 C4
R0 25  2 77 85 72
R1 71 92 98 87 53
R2 35 29 82 65 20
R3  2 29 66 42 12
R4 99 72 78 30 11
val x : Dense.dsmat =
```

`Dense` module also provides other functions to create various matrices, e.g., as below.

```ocaml
let x = Dense.eye 5;;             (* identity matrix *)
let x = Dense.zeros 5 5;;         (* all elements are zeros *)
let x = Dense.ones 5 5;;          (* all elements are ones *)
let x = Dense.uniform 5 5;;       (* random matrix of uniform distribution *)
let x = Dense.gaussian 5 5;;      (* random matrix of gaussian distribution *)
...
```

Combined with `Stats` module, you can also create any matrices of many distributions. E.g., the following code first creates an empty dense matrix, then initialise the elements with Bernoulli distribution. Test it in `utop`, you should get a dense matrix where half of the elements are zeros.

```ocaml
let x = Dense.empty 8 8 |> Dense.map (fun _ -> Stats.Rnd.bernoulli 0.5 |> float_of_int);;
```

With `Dense` module, you can also generate linearly spaced interval and meshgrids, as below.

```ocaml
let x = Dense.linspace 0. 5. 6;;
   C0  C1  C2  C3  C4  C5
R0  0   1   2   3   4   5
val x : Dense.dsmat =
```



## Conclude
