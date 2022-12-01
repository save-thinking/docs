# CSS framework

Contents:

* [Summary](#summary)
  * [Issue](#issue)
  * [Decision](#decision)
  * [Status](#status)
* [Details](#details)
  * [Assumptions](#assumptions)
  * [Constraints](#constraints)
  * [Positions](#positions)
  * [Argument](#argument)
* [Related](#related)
  * [Related decisions](#related-decisions)
  * [Related requirements](#related-requirements)
  * [Related principles](#related-principles)
* [Notes](#notes)


## Summary


### Issue

We want to use a CSS framework for our web application:

  * We want the user experience to be fast and reliable.

  * We want intuitive design, which is easy to understand and follow.

    


### Decision

Decided on Tailwind.


### Status

Decided on Tailwind against normal CSS.

## Details


### Assumptions

We want our application to be intuitive, simple and fast.

We want our app to be scalable and focus more on its intuitive design rather than focusing on the boilerplate css code, tailwind serves this purpose by providing the base level of styling and allows us to add customisations.



### Constraints

Tailwind offers limited styling components. 

Though the current set of components is enough for our application at this point, for more complex UI/UX, it has some limitations.


### Positions

We considered the following options for CSS: Bootstrap, Tailwind CSS and Vanilla CSS. 

Tailwind CSS is basically a Utility first CSS framework for building rapid custom UI. It is a highly customizable, low-level CSS framework that gives base styling to work upon.

Example with Tailwind CSS:

```html
<div class="p-6 hover:bg-green-600
                    hover:text-white transition
                    duration-300 ease-in">
 
            <h1 class="text-2xl font-semibold mb-3">
                Hover
            </h1>
</div>
```


Example with Bootstrap:
```html
<div>
 
            <h1 class="row highlight">
                Hover
            </h1>
</div>
```

```
.row.highlight:hover {
    background-color: #123456;
}
```


Example with Vanilla CSS:
```
:hover {
  css declarations;
}
```
### Argument

Specifically, Tailwind CSS helps us customise the components by providing the base CSS properties. No separate overhead to maintain the css files. It is also resposive and stable and for the scope of the project, it provided all the components we needed for the UI/UX.



## Related


### Related decisions

The CSS framework we choose may affect testability.


### Related requirements

We want to ship a purely-modern app fast without compromising on the quality. 

We do not want to spend time working on boilerplate css and tailwind helped us achieve this by providing the base to styling components.



### Related principles

Tailwind has been known to be stable and fast, which is exactly what we needed for our application.


## Notes

Any notes here.
