---
title: Angular Components Introduction
layout: default
---

## Angular Components Introduction

### What is an Angular component?

The following was summarized from Angular Docs > Fundamentals > [Architecture](https://angular.io/guide/architecture#components)

A *component* controls a patch of screen (display, UI surface, rectangle) called a *view*. 

As code, a component is a class, with a decorator.

The class is JavaScript, specifically TypeScript. It includes all the code needed for the the component's *behaviour* during its lifetime.

A decorator is a function that modifies a class. It has one parameter, which is an object composed of configuration information as key-value pairs. This object is *metadata*, and the Angular runtime uses the metadata when initializing the component. 

One of the decorator's properties is a *template*, defines the *appearance* of the component. The template includes HTML, or the name of an HTML file. By definition, HTML is the language of the Angular template. Almost all HTML elements are valid in a template, except for these: `html`, `body`, `base`, and `script`.

Another decorator property is the *selector*. Its value is the name of the custom HTML element in the *parent* template that becomes the component. 

In summary, from the Angular documentation's Fundamentals > Architecture guide:

*The template, metadata, and component together describe a view.*

![Component code + template + metadata = a view](https://angular.io/generated/images/guide/architecture/template-metadata-component.png)

How does the MVC (or MVVM) design patterns map to Angular? Well, in Angular:

The *component* has the code for the *controller* and the *view model*. 

The *template* has the code for the *view*. 

### Quick Review - Creating an Angular Project from Scratch

Before we start writing components, we should get a new Angular project going.  Recall, from week 6:

1. Create a new directory somewhere on your local machine and open it in Visual Studio Code.

2. Using the "Integrated Terminal", create a new app (assuming that you want to create a new app (and folder) named “my-dream-app”), ie:

  ```
  ng new my-dream-app --routing -st
  ```
  
  **Note:** 
  
  The `--routing` option adds the code we need for "routing", which is a topic that will be covered in detail next week. Adding routing now (when the new project is created) is a *best practice*. 

The `-st` option does not add "testing" code. One of the effects is that it reduces the size of the project, and makes it slightly faster in the change detection and build processes.
  
Finally, change your working directory to the newly created folder and start the server listener, ie:

```
cd my-dream-app
ng serve --open
```

### Creating a Component from Scratch (Using "ng generate")

Recall, from the Angular "Tour of Heroes" app, we can manually create a component using the following steps

1. Stop the server listener in the integrated terminal (ctrl + c) and execute the command:

```
ng generate component foo --flat
```

**Note:**

The "--flat" flag will NOT create a folder to enclose the component's source code files. We'll use that for the first while, until the number of files in the app folder gets too unreasonable.

> Documentation for the `ng generate component` command is [here](https://github.com/angular/angular-cli/wiki/generate-component). 

Using "ng generate" to create the "foo" component for us has saved us time by automating the following (necessary) steps:

* Created the files: **foo.component.css**, **foo.component.html**, **foo.component.ts** (including the correct class, and "@Component" decorator to make use of the .html &amp; .css files / providing a default "app-" selector property) and lastly, **foo.component.spec.ts** (we can remove this file if we used the "-st" option when creating the project, since we are not interested in testing at the moment)

* Added the correct "import" statement to app.module.ts, ie:

```
import { FooComponent } from './foo.component';
```

* Added "FooComponent" to the "@NgModule" decoration in app.module.ts, ie:

```
@NgModule({
  declarations: [
    AppComponent,
    FooComponent //Added!
  ],
  imports: [
    BrowserModule,
    AppRoutingModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

### Including the New Component

Recall the "selector" property that was automatically added, ie "app-foo".  This corresponds to the custom element `<app-foo></app-foo>` that we can use to render our newly created "foo" component.

To see this in action, add the `<app-foo></app-foo>` element to the bottom of your **app.component.html** file and "serve" your application again, if it's not already running.

You should now see the text "foo works" at the bottom of the default "start" page.

### How to think about and plan your components

Now that we are comfortable adding new (simple) components, why don't we try creating a view using *multiple* components.  

> The content for this discussion can be found in ["Angular Components Example"](angular-components-example)

### Using "Templates" in your components

From the example above, we have seen how we can add multiple components as children of a parent component.  However, these were simply "static" components (ie: their content is hardcoded into the .html).  If we wish our "template" (.html file) to reference values within its corresponding component, we need to reference them using the following techniques:

* [Interpolation](https://angular.io/guide/template-syntax#interpolation----)
* [Template Expressions](https://angular.io/guide/template-syntax#template-expressions) / [Property Binding](https://angular.io/guide/template-syntax#property-binding--property-)
* [Template Statements](https://angular.io/guide/template-syntax#template-statements)
* [Attribute, class, and style bindings](https://angular.io/guide/template-syntax#attribute-class-and-style-bindings)

Essentially, the above logic is really referring to specific types of ["Binding Syntax"](https://angular.io/guide/template-syntax#binding-syntax-an-overview). 

Note:  We will save ["Two-way binding"](https://angular.io/guide/template-syntax#two-way-binding---) until we discuss forms in Angular.

<br>

#### Quick Directive Overview

[https://angular.io/guide/attribute-directives#directives-overview](https://angular.io/guide/attribute-directives#directives-overview)

**Built In Directives**

* [Built-in attribute directives](https://angular.io/guide/template-syntax#built-in-attribute-directives)
* [Built-in structural directives](https://angular.io/guide/template-syntax#built-in-structural-directives) (ie, \*ngIf / \*ngFor, etc.)

**Building a simple "attribute" directive**

* [Build a simple attribute directive](https://angular.io/guide/attribute-directives#build-a-simple-attribute-directive)

<br>

