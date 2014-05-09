!SLIDE center
# Wat
![WAT](./wat.png "wat")

!SLIDE bullets incremental
# Terminologie
* Integration
* Units
* TDD
* BDD
* The Three laws of TDD

!SLIDE bullets incremental
# Integration
* "It must be a rooster"
* "It must have an eye"
* "It must be 30mm wide, 90mm deep and 80mm high"

!SLIDE center
![integration](duplo.jpg)

!SLIDE bullets incremental
# Units
* "It must be green"
* "It must have four knobs"
* "It must have one rounded edge"
* "It must be 30mm wide, 45mm deep and 20mm high"

!SLIDE center
![unit](duplo_unit_B.jpg)

!SLIDE bullets incremental
# Units and Integration
* Units kunnen veranderen
* Behaviour blijft hetzelfde

!SLIDE center
![different unit](duplo_integration_swap_units.jpg)

!SLIDE bullets incremental
# Omarm verandering
* Units kunnen herschreven worden.
* Maar aan de buitenkant blijft het hetzelfde werken. 
* Dat weet je "zeker", als je integrationtest groen is.
* (Voor alles wat je met die integrationtests test)

!SLIDE bullets incremental
# TDD: Test Driven development
* Schrijf eerst de tests
* En dan pas de code voor die test

!SLIDE bullets incremental
# BDD: Behaviour Driven development
* Variatie op TDD
* Schrijf eerst de gewenste uitkomst
* Test eerst de integratie (het gedrag)

!SLIDE
# Three Laws
> You are not allowed to write any production code unless it is to make a failing unit test pass.

!SLIDE
# Three Laws
> You are not allowed to write any more of a unit test than is sufficient to fail; and compilation failures are failures.

!SLIDE
# Three Laws
> You are not allowed to write any more production code than is sufficient to pass the one failing unit test.

