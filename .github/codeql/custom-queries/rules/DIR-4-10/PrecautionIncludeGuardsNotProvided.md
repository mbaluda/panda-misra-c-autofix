# Dir 4.10: Precautions shall be taken in order to prevent the contents of a header file being included more than once

This query implements the MISRA C 2012 Directive 4.10:
> Precautions shall be taken in order to prevent the contents of a header file being included more than once.

## Classification
<table>
<tr><td><b>Category</b></td><td>Required</td></tr>
<tr><td><b>Applies to</b></td><td>C90, C99, C11</td></tr>
</table>

## Rationale
When a translation unit contains a complex hierarchy of nested header files, it is possible for a particular header file to be included more than once. This can be, at best, a source of confusion. If this multiple inclusion leads to multiple or conflicting definitions, then this can result in undefined or erroneous behaviour.

## Example
```c
/* file.h */
#ifndef FILE_H
/* Non-compliant - does not #define FILE_H */
#endif
```

The following examples show two ways by which the contents of a header file could be protected from being included more than once in a translation unit, but this is not an exclusive list.

**Example 1**
```c
<start-of-file>
#if !defined ( identifier )
#define identifier
/* Contents of file */
#endif
<end-of-file>
```

**Example 2**
```c
<start-of-file>
#ifndef identifier
#define identifier
  /* Contents of file */
#endif
<end-of-file>
```

## Agentic Autofix
When generating a fix for this alert, follow the [instructions for CodeQL Coding Standards](https://github.com/github/codeql-coding-standards/blob/mbaluda-autofix/docs/autofix-instructions.md). These instructions also describe how to handle false-positive exclusions through deviations scoped at the line, file, or project level.

_Notes:_
1. The identifier used to test and record whether a given header file has already been included shall be unique across all header files in the project.
2. Comments are permitted anywhere within these forms.