# 2025-06-iifosf

### General overview:

1.  bsvars.org is a family of packages for structural and predictive analyses using Bayesian Structural VARs
2.  bsvars and bsvarSIGNs are two packages out on CRAN
3.  SVAR equations and dot points on main assumptions
4.  State the purposes of working with these models
5.  Identification in both packages
6.  Modelling features and references(?)

### Six slides on how it's working:

1.  model specification (just specification code)
2.  estimation (code and progress bar)
3.  forecasting (code line and plot)
4.  FEVDs (code line and plot)
5.  IRFs (code line and plot)
6.  HDs (code line and plot)

### Target audience

1.  academic researchers (reproducibility, transparency, literature context)
2.  PhD students (communication via email/GH issues, extendability, up-to date with the newest developments)
3.  master students (simple workflows, documentation and examples, video presentations)
4.  applied economists at economic governance institutions (reliability, speed, incorporating feedback on new features)
5.  institutions (integration with their workflows, output reporting practices, off-the-shelf applications)

### Alignment with researcher's objectives \[skip this\]

1.  priority given to research-driven software (research dissemination, set a balance between providing code for your research and accommodating modelling/forecasting practices representing broader field)
2.  a package must result in academic publication (streamlining)
3.  schedule: package release/working paper/journal submission and R&Rs/package journal submission
4.  incorporate working on the package in the research project development (make the package-related overheads minimal by being good at doing these things)
5.  as an econometrician on a project, if you develop a package your co-authors are more likely (keen on) doing the empirical analysis (so, it's not all on you)
6.  Secure presentation outlets for package promotion in academic and non-academic setup
7.  leverage the package/paper release to boost your engagement (research application in non-academic context)

- promote the package to facilitate spontaneous user applications
- reach out to essential institutions
- seek

8.  Manage IP: the easiest if packages developed with own PhD students, manageable otherwise

### Design features

1.  combine the best of two worlds:

- speed of algorithms written using compiled code, C++
- convenience of data analysis using interpreted code, R

2.  reasons to choose Rcpp (over C)

- provide essential functionality for package development
- manageable dependencies combined with good communication by Rcpp developers
- simplicity in package setup/compilation/linking/assuring object compatibility lowering the (perceived) entry requirements
- great support (Dirk replies the following Canadian morning to #rcpp)
- super fast on loops (Gibbs sampler is a serial job)
- parallel computations using openMP (independent sampler, to be implemented - we struggle with reproducibility of RNGs)

3.  reasons to rely on RcppArmadillo

- frontier package for linear algebra (speed, speed, speed)
- fast and reproducible RNGs
- excellent documentation and support in package development
- makes C++ code as expressive as R

4.  R6 management of the input object (give some code examples here):

- minimal scripting `specify_bsvar*$new()` provides basic setup of: starting values, identification, data matrices, prior hyper-parameters (each of them are lists with R6 structure)
- ample modeling choices managed by arguments of `specify_bsvar*$new()`
- possibility of coherent customisation using in functions R6 public elements
- essential specification variables managed by R6 private elements

5.  combining simple workflows and transparency on what model we work on using S3 generics and methods (give example of `estimate`)
6.  Interpackage: Establish a set of generics in bsvars and provide model-specific methods over different packages - assure similar workflows - use `Depends:` and `Imports:`
7.  Interpackage: export all C++ functions in a library, so other developers have access to everything for their R packages with C++ code

- use `LinkingTo` and `Depends:`
- pointer management
- consistency in object declarations (th use of `const`)
- assignment by reference not working
- mysterious working of `[[Rcpp:interface(cpp)]]` - does not export al C++ function for some reason

9.  Outputs and workflows:

- Provide all the outputs (posterior draws), so that insightful users can can compute demanded outputs not provided in package
- Provide all the basic functionality with well-designed workflows, `plot` and `summary` for users valuing simplicity in scripting "It's amazing how much you do with a few lines of code!"

10. Extensive resources:

- documentation pitched to users of various level of advancement (explain basics what's Gibbs sampler and thinning, as well as advanced features state model equations and provide references)
- pkgdown website with package features, social media chanells, and updates on the most recent presentations!
- Write up a vignette that will be sent to JSS or the R Journal (once the methodological paper is published)

## Future developments

1.  **bvarPANELs** - Bayesian forecasting of labour market outcomes for the ILO
2.  **bsvarTVPs** with Annika - Time-varying identification of Structural VARs as an extension to **bsvars**
3.  **bsvarCFs** with Dan - Bayesian forecasting with VARs subject to soft and hard restrictions as an extension to **bsvars** and **bsvarSIGNs**
4.  **bvarNWish** with Andres and Rui - Bayesian forecasting with VARs with flexible shrinkage
5.  **bsmars** with Loncan - Bayesian forecasting with Matrix Autoregressions