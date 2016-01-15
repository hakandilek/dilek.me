---
layout:     post
title:      UML diagrams for Jekyll and Markdown
date:       2016-01-15 18:00:00
summary:    Integrating UML diagrams into Github Markdown and Jekyll based static web sites
categories: UML PlantUML markdown
---

It is possible to embed UML diagrams into Jekyll or Markdorn pages using the [Gravizo](http://www.gravizo.com/) image generation service.

You don't have to install any local Gems or plugins to embed such diagrams in your Jakyll pages.

Here are some sample UML diagrams:

#### Class diagram

![Alt text](http://g.gravizo.com/g?
@startuml;
Object <|-- ArrayList;
Object : equals%28%29;
ArrayList : Object[] elementData;
ArrayList : size%28%29;
@enduml
)


#### Sequence diagram

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
