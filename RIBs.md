# RIBs

  - MVC, MVP, MVI, MVVM and VIPER are architecture patterns. RIBs is a framework. 


### What differentiates RIBs from frameworks based on MV*/VIPER is:

Business logic drives the app, not the view tree. Unlike with MV*/VIPER, a RIB does not have to have a view. 
This means that the app hierarchy is driven by the business logic, not the view tree.
Independent business logic and view trees. RIBs decouple how the business logic scopes are structured from view hierarchies.
This allows the application to have a deep business logic tree, isolating business logic nodes, while maintaining a shallow view hierarchy making layouts, animations and transitions easy.
