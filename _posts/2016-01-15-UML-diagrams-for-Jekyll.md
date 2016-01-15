---
layout:     post
title:      UML diagrams for Jekyll
date:       2016-01-15 18:00:00
summary:    Integrating UML diagrams into Jekyll based static web sites
categories: Jekyll UML PlantUML
---

It is possible to embed UML diagrams into Jekyll sites using the [jekyll-plantuml Plugin](https://github.com/yegor256/jekyll-plantuml) plugin.

You have to update following files and insert the `gem` definitions:

#### config.yml:
```yaml
# Gems
gems: ['jekyll-plantuml', ... other gems... ]
```

#### Gemfile:
```ruby
gem 'jekyll-plantuml'
```

After successfull compilation, you should see an UML diagram like the following here:

![Alt text](http://g.gravizo.com/g?
@startuml;
Object : equals%28%29
ArrayList : Object%5B%5D elementData
ArrayList : size%28%29
@enduml)

![Alt text](http://g.gravizo.com/g?
@startuml;
actor User;
participant "First Class" as A;
participant "Second Class" as B;
participant "Last Class" as C;
User -> A: DoWork;
activate A;
A -> B: Create Request;
activate B;
B -> C: DoWork;
activate C;
C --> B: WorkDone;
destroy C;
B --> A: Request Created;
deactivate B;
A --> User: Done;
deactivate A;
@enduml)
