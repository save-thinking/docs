# JS Minifier

Contents:

- [JS Minifier](#js-minifier)
  - [Summary](#summary)
    - [Issue](#issue)
    - [Decision](#decision)
    - [Status](#status)
  - [Details](#details)
    - [Assumptions](#assumptions)
    - [Constraints](#constraints)
    - [Positions](#positions)
    - [Argument](#argument)
    - [Implications](#implications)
  - [Related](#related)
    - [Related decisions](#related-decisions)
    - [Related requirements](#related-requirements)
    - [Related artifacts](#related-artifacts)
    - [Related principles](#related-principles)
  - [Notes](#notes)


## Summary


### Issue

We want to remove my dependency on module and and have a single src file which loads all the dependencies:

  * We want to compiles to one minified linked JS file that can used inside of a \<script\> tag.

  * We want the tool have the option of --watch to auto-link and compile so that local development cycle is fast.

  * We want tt be simple and not configuration complexity


### Decision

Not Decided


### Status

In progress


## Details


### Assumptions

We want to an automation tool to combine all the JS files into a single file and minify them. 



### Constraints

We want an up-to-date and stable minify tool. 

If we choose a minify tool that haven't updated for a long time, then we might get into trouble when minify code using new JS features.

If we choose a unstable minify tool, then our product will not be stable. 


### Positions

We considered babel-minify as it can use Babel's toolchain for compilation. Babel-minify will have tight integration with the rest of the babel ecosystem. Babel-minify would also be able to use the same cache as the rest of the babel plugins, if caching enabled through for example babel-loader. However, after further searching, we found babel-minify is still in 0.x and not recommended to be used in production by the development team. 

We considered uglify-JS but it only supports ES5 code as input.

We considered uglify-es but it is buggy according to the communities and also no longer maintained.

We considered Google Closure Compiler as it is both maintaining and support ES6+. Google Closure Compiler also suppor API calls from JS files. Using the whole JS files in the P0 product as the testing files, Closure Compiler takes 875 Milliseconds and output file is 101KB.

We considered Terser as it is both maintaining and support ES6+. Terser also suppor API calls from JS files. Terser also provide source map option when compressing multiple JS files into a single file. This would be highly useful for debugging. Terser also suppor mangle option to mangle the names excpet all customized reversed name. If we use this feature, we can increase the safty and privacy of our code. 

Here is the performance test for Google Closure Compiler and Terser.
| Artifact                                                                                                                          |                    Original size |                            |
| :-------------------------------------------------------------------------------------------------------------------------------- | -------------------------------: | ------------------------------: | --------------------------: |
| [P0 product](https://github.com/save-thinking/group-1-save-thinking/pull/48) |                       `240.43 kB` |                             |
| **Minifier**                                                                                                                      |                **Minified size** |              **Time** |
| [google-closure-compiler]([/lib/minifiers/google-closure-compiler.ts](https://github.com/google/closure-compiler))                                                              |       <sup>-58% </sup>`100.13 kB` |<sup>*3x* </sup>`875 ms` 
| [terser]([/lib/minifiers/terser.ts](https://github.com/terser/terser))                                                                                                |       <sup>-34% </sup>`158.75` |   <sup>*1x* </sup>`313 ms` |


### Argument

I recommended choosing Terser

Extreme compressing size is not our priority at the moment. The source map function in mangle can let us more easy to debug, and mangle option would produce a more secured product. 


### Implications

A fast and efficiency minifier can help us save bandwidth and decrease load time. 


## Related


### Related decisions

The minifier tool we choose will affect product's performance and debuging ability.


### Related requirements

We want support for modern ES6+. We want our product easy to debug.


### Related artifacts

Affects all JS file.


### Related principles

Easily reversible.

Need for speed.

Easily debug.

## Notes

Any notes here.
