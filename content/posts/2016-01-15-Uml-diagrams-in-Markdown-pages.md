---
layout:     post
title:      UML diagrams for Jekyll and Markdown
date:       2016-01-15 13:00:00
summary:    Integrating UML diagrams into Github Markdown and Jekyll based static web sites
categories: UML PlantUML markdown
---


***Update: 2020-05-05: Although it was possible to embed plantuml diagrams into markdown. As of today this does not seem to work wiithout URL encoding the PlantUml content.***

It is possible to embed UML diagrams into Jekyll or Markdorn pages using the [Gravizo](http://www.gravizo.com/) image generation service.

You don't have to install any local Gems or plugins to embed such diagrams in your Jakyll pages.

Here are some sample UML diagrams:

#### Class diagram

```Markdown
![Alt text](http://g.gravizo.com/svg?
@startuml;
Object <|-- ArrayList;
Object : equals%28%29;
ArrayList : Object[] elementData;
ArrayList : size%28%29;
@enduml
)
```

![Alt text](http://g.gravizo.com/svg?%20@startuml;%20Object%20%3C|--%20ArrayList;%20Object%20:%20equals%28%29;%20ArrayList%20:%20Object[]%20elementData;%20ArrayList%20:%20size%28%29;%20@enduml)


#### Sequence diagram

```Markdown
![Alt text](http://g.gravizo.com/svg?
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
```

![Alt text](http://g.gravizo.com/svg?%20@startuml;%20actor%20User;%20participant%20%22First%20Class%22%20as%20A;%20participant%20%22Second%20Class%22%20as%20B;%20participant%20%22Last%20Class%22%20as%20C;%20User%20-%3E%20A:%20DoWork;%20activate%20A;%20A%20-%3E%20B:%20Create%20Request;%20activate%20B;%20B%20-%3E%20C:%20DoWork;%20activate%20C;%20C%20--%3E%20B:%20WorkDone;%20destroy%20C;%20B%20--%3E%20A:%20Request%20Created;%20deactivate%20B;%20A%20--%3E%20User:%20Done;%20deactivate%20A;%20@enduml)
