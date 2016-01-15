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

Object <|-- ArrayList

Object : equals()
ArrayList : Object[] elementData
ArrayList : size()

@enduml
)
