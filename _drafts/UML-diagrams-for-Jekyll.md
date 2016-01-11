---
layout:     post
title:      UML diagrams for Jekyll
date:       2016-01-12 22:00:00
summary:    Integrating UML diagrams into Jekyll based static web sites
categories: Jekyll UML PlantUML
---

Using [jekyll-plantuml Plugin](https://github.com/yegor256/jekyll-plantuml)

config.yml: 
```
# Gems
gems: ['jekyll-plantuml', ... other gems... ]
```

Gemfile:
```
gem 'jekyll-plantuml'
```


@startuml
Object <|-- ArrayList

Object : equals()
ArrayList : Object[] elementData
ArrayList : size()

@enduml
