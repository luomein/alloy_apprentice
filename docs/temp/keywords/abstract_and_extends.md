# `abstract` and `extends`
* [Extensions of the same signature are mutually disjoint](http://homepage.divms.uiowa.edu/~tinelli/classes/5810/Fall22/Notes/03.1-intro-to-alloy.pdf)
* [All extensions of an abstract signature `A` form a partition of `A`](http://homepage.divms.uiowa.edu/~tinelli/classes/5810/Fall22/Notes/03.1-intro-to-alloy.pdf)
* All extensions of a non-abstract signature `A` ***do not*** form a partition of `A`
## Single sig extends
### extends an abstract sig
    abstract sig A{}
    sig A_extends extends A{}

    check {
      no a : A  |  not a in A_extends
      all a : A |   a in A_extends
      all a : univ | a in A <=> a in A_extends
      A = A_extends
    }
### extends a non-abstract sig
    sig A{}
    sig A_extends extends A{}

    fact {
      some a : A | not a in A_extends
    }

    check {
      some a : A | not a in A_extends
      A != A_extends
    }
## Multiple sig extends
### extends an abstract sig
    abstract sig A{}
    sig A1_extends, A2_extends extends A{}

    check {
      A = ( A1_extends + A2_extends)
    }
### extends a non-abstract sig
    sig A{}
    sig A1_extends, A2_extends extends A{}

    fact {
      some a : A | not a in  ( A1_extends + A2_extends )
    }

    check {
      A != ( A1_extends + A2_extends)
    }
