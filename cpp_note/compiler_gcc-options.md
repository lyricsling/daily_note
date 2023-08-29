---
tags: [Notebooks/Cpp]
title: gcc
created: '2023-08-16T03:35:34.033Z'
modified: '2023-08-16T03:43:08.052Z'
---

# gcc

## gcc警告

### -Wall
开启警告,这些都是容易产生以及容易解决的警告
```bash
-Waddress
-Warray-bounds=1 (only with -O2)
-Warray-compare
-Warray-parameter=2 (C and Objective-C only)
-Wbool-compare
-Wbool-operation
-Wc++11-compat  -Wc++14-compat
-Wcatch-value (C++ and Objective-C++ only)
-Wchar-subscripts
-Wcomment
-Wdangling-pointer=2
-Wduplicate-decl-specifier (C and Objective-C only)
-Wenum-compare (in C/ObjC; this is on by default in C++)
-Wenum-int-mismatch (C and Objective-C only)
-Wformat
-Wformat-overflow
-Wformat-truncation
-Wint-in-bool-context
-Wimplicit (C and Objective-C only)
-Wimplicit-int (C and Objective-C only)
-Wimplicit-function-declaration (C and Objective-C only)
-Winit-self (only for C++)
-Wlogical-not-parentheses
-Wmain (only for C/ObjC and unless -ffreestanding)
-Wmaybe-uninitialized
-Wmemset-elt-size
-Wmemset-transposed-args
-Wmisleading-indentation (only for C/C++)
-Wmismatched-dealloc
-Wmismatched-new-delete (only for C/C++)
-Wmissing-attributes
-Wmissing-braces (only for C/ObjC)
-Wmultistatement-macros
-Wnarrowing (only for C++)
-Wnonnull
-Wnonnull-compare
-Wopenmp-simd
-Wparentheses
-Wpessimizing-move (only for C++)
-Wpointer-sign
-Wrange-loop-construct (only for C++)
-Wreorder
-Wrestrict
-Wreturn-type
-Wself-move (only for C++)
-Wsequence-point
-Wsign-compare (only in C++)
-Wsizeof-array-div
-Wsizeof-pointer-div
-Wsizeof-pointer-memaccess
-Wstrict-aliasing
-Wstrict-overflow=1
-Wswitch
-Wtautological-compare
-Wtrigraphs
-Wuninitialized
-Wunknown-pragmas
-Wunused-function
-Wunused-label
-Wunused-value
-Wunused-variable
-Wuse-after-free=2
-Wvla-parameter (C and Objective-C only)
-Wvolatile-register-var
-Wzero-length-bounds
```

### -Wextra
开启除 Wall 外的一些额外警告
```bash
-Wclobbered
-Wcast-function-type
-Wdeprecated-copy (C++ only)
-Wempty-body
-Wenum-conversion (C only)
-Wignored-qualifiers
-Wimplicit-fallthrough=3
-Wmissing-field-initializers
-Wmissing-parameter-type (C only)
-Wold-style-declaration (C only)
-Woverride-init
-Wsign-compare (C only)
-Wstring-compare
-Wredundant-move (only for C++)
-Wtype-limits
-Wuninitialized
-Wshift-negative-value (in C++11 to C++17 and in C99 and newer)
-Wunused-parameter (only with -Wunused or -Wall)
-Wunused-but-set-parameter (only with -Wunused or -Wall)
```

### -Weffc++
开启 effective c++ 中规范警告

### -Wshadow
全局变量覆盖了局部变量的警告

### -Wpedantic
ISO c++ 的警告

### -Wconversion
变量隐式转化，可能引起值发生变化时，发出警告

### -Wsign-conversion
无符号和有符号值转化时发出警告
