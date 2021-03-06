---
title: 2-5-python-文档资源
url: 2-5-python-文档资源
author: YJ2CS
avatar: '/custom/avatar.webp'
authorLink: YJ2CS.github.io
authorAbout: 愿青年摆脱了冷气，只是向前走！
authorDesc: 愿青年摆脱了冷气，只是向前走！
comments: true
categories:
  - 文章
tags:
  - 悦读
no-photos: 'https://random.52ecy.cn/randbg.php?size=1&rid-2-5-python-文档资源'
date: 2020-12-20 00:30:05
---



# 1. Python 文档资源  
## 1.1 # 注释  
井号注释是代码编写文档的最基本方式。Python 会忽略 # 之后所有文字（只要 # 不是位于字符串常量中）。# 注释最适用于较小功能的文档。  

## 1.2 dir 函数  
内置的 dir 函数是抓取对象内可用所有属性列表的简单方式（例如，对象的方法以及较简单的数据项）。它能够调用任何有属性的对象。

```python
import sys
dir(sys)
```

    ['__displayhook__',
     '__doc__',
     '__excepthook__',
     '__interactivehook__',
     '__loader__',
     '__name__',
     '__package__',
     '__spec__',
     '__stderr__',
     '__stdin__',
     '__stdout__',
     '_clear_type_cache',
     '_current_frames',
     '_debugmallocstats',
     '_enablelegacywindowsfsencoding',
     '_getframe',
     '_git',
     '_home',
     '_xoptions',
     'api_version',
     'argv',
     'base_exec_prefix',
     'base_prefix',
     'builtin_module_names',
     'byteorder',
     'call_tracing',
     'callstats',
     'copyright',
     'displayhook',
     'dllhandle',
     'dont_write_bytecode',
     'exc_info',
     'excepthook',
     'exec_prefix',
     'executable',
     'exit',
     'flags',
     'float_info',
     'float_repr_style',
     'get_asyncgen_hooks',
     'get_coroutine_wrapper',
     'getallocatedblocks',
     'getcheckinterval',
     'getdefaultencoding',
     'getfilesystemencodeerrors',
     'getfilesystemencoding',
     'getprofile',
     'getrecursionlimit',
     'getrefcount',
     'getsizeof',
     'getswitchinterval',
     'gettrace',
     'getwindowsversion',
     'hash_info',
     'hexversion',
     'implementation',
     'int_info',
     'intern',
     'is_finalizing',
     'maxsize',
     'maxunicode',
     'meta_path',
     'modules',
     'path',
     'path_hooks',
     'path_importer_cache',
     'platform',
     'prefix',
     'ps1',
     'ps2',
     'ps3',
     'set_asyncgen_hooks',
     'set_coroutine_wrapper',
     'setcheckinterval',
     'setprofile',
     'setrecursionlimit',
     'setswitchinterval',
     'settrace',
     'stderr',
     'stdin',
     'stdout',
     'thread_info',
     'version',
     'version_info',
     'warnoptions',
     'winver']

要找出内置对象类型提供了哪些属性，可运行 dir 并传入所需要类型的常量：

```python
dir([])
```

    ['__add__',
     '__class__',
     '__contains__',
     '__delattr__',
     '__delitem__',
     '__dir__',
     '__doc__',
     '__eq__',
     '__format__',
     '__ge__',
     '__getattribute__',
     '__getitem__',
     '__gt__',
     '__hash__',
     '__iadd__',
     '__imul__',
     '__init__',
     '__init_subclass__',
     '__iter__',
     '__le__',
     '__len__',
     '__lt__',
     '__mul__',
     '__ne__',
     '__new__',
     '__reduce__',
     '__reduce_ex__',
     '__repr__',
     '__reversed__',
     '__rmul__',
     '__setattr__',
     '__setitem__',
     '__sizeof__',
     '__str__',
     '__subclasshook__',
     'append',
     'clear',
     'copy',
     'count',
     'extend',
     'index',
     'insert',
     'pop',
     'remove',
     'reverse',
     'sort']

任何内置类型的 dir 结果都包含了一组属性，这些属性和该类型的实现相关；就像在模块中一样，它们都以双下划线开始和结束，从而保证了其独特性。

```python
len(dir([])), len([x for x in dir([]) if not x.startswith('__')])
```

    (46, 11)

此外，也可以把类型的名称传给 dir，而不是常量，依然可以得到相同的结果。

```python
dir(str) == dir('')
```

    True

## 1.3 文档字符串：__doc__  
Python 支持可自动附加在对象上的文档，而且在运行时还可保存查看。  

从语法上来说，这类注释是写成字符串，放在模块文件、函数以及类语句的顶端，在任何可执行程序代码前。  

Python 会自动封装这个字符串，使其成为相应对象的 `__doc__` 属性。  

**用户定义的文档字符串**  
文档字符串出现在文件开端以及其中的函数和类的开头。

```python
"""
Module documentation
Words Go Here
"""

spam = 40

def square(x):
    """
    function documentation
    can we have your liver then?
    """
    return x ** 2

class Employee:
    "class documentation"
    pass

print(square(4))
print(square.__doc__)
```

    16
    
        function documentation
        can we have your liver then?

    

注释会保存在 `__doc__` 属性中以供查看（文件导入之后）。

```python
import docstring
```

    16
    
        function documentation
        can we have your liver then?

  

```python
print(docstring.__doc__)
```

    Module documentation
    Words Go Here

```python
print(docstring.square.__doc__)
```

        function documentation
        can we have your liver then?

```python
print(docstring.Employee.__doc__)
```

    class documentation

**内置文档字符串**  
Python 中的内置模块和对象都使用类似的技术，在 dir 返回的属性列表前后加上文档。

```python
import sys
print(sys.__doc__)
```

    This module provides access to some objects used or maintained by the
    interpreter and to functions that interact strongly with the interpreter.
    
    Dynamic objects:
    
    argv -- command line arguments; argv[0] is the script pathname if known
    path -- module search path; path[0] is the script directory, else ''
    modules -- dictionary of loaded modules
    
    displayhook -- called to show results in an interactive session
    excepthook -- called to handle any uncaught exception other than SystemExit
      To customize printing in an interactive session or to install a custom
      top-level exception handler, assign other functions to replace these.
    
    stdin -- standard input file object; used by input()
    stdout -- standard output file object; used by print()
    stderr -- standard error object; used for error messages
      By assigning other file objects (or objects that behave like files)
      to these, it is possible to redirect all of the interpreter's I/O.
    
    last_type -- type of last uncaught exception
    last_value -- value of last uncaught exception
    last_traceback -- traceback of last uncaught exception
      These three are only available in an interactive session after a
      traceback has been printed.
    
    Static objects:
    
    builtin_module_names -- tuple of module names built into this interpreter
    copyright -- copyright notice pertaining to this interpreter
    exec_prefix -- prefix used to find the machine-specific Python library
    executable -- absolute path of the executable binary of the Python interpreter
    float_info -- a struct sequence with information about the float implementation.
    float_repr_style -- string indicating the style of repr() output for floats
    hash_info -- a struct sequence with information about the hash algorithm.
    hexversion -- version information encoded as a single integer
    implementation -- Python implementation information.
    int_info -- a struct sequence with information about the int implementation.
    maxsize -- the largest supported length of containers.
    maxunicode -- the value of the largest Unicode code point
    platform -- platform identifier
    prefix -- prefix used to find the Python library
    thread_info -- a struct sequence with information about the thread implementation.
    version -- the version of this interpreter as a string
    version_info -- version information as a named tuple
    dllhandle -- [Windows only] integer handle of the Python DLL
    winver -- [Windows only] version number of the Python DLL
    _enablelegacywindowsfsencoding -- [Windows only] 
    __stdin__ -- the original stdin; don't touch!
    __stdout__ -- the original stdout; don't touch!
    __stderr__ -- the original stderr; don't touch!
    __displayhook__ -- the original displayhook; don't touch!
    __excepthook__ -- the original excepthook; don't touch!
    
    Functions:
    
    displayhook() -- print an object to the screen, and save it in builtins._
    excepthook() -- print an exception and its traceback to sys.stderr
    exc_info() -- return thread-safe information about the current exception
    exit() -- exit the interpreter by raising SystemExit
    getdlopenflags() -- returns flags to be used for dlopen() calls
    getprofile() -- get the global profiling function
    getrefcount() -- return the reference count for an object (plus one :-)
    getrecursionlimit() -- return the max recursion depth for the interpreter
    getsizeof() -- return the size of an object in bytes
    gettrace() -- get the global debug tracing function
    setcheckinterval() -- control how often the interpreter checks for events
    setdlopenflags() -- set the flags to be used for dlopen() calls
    setprofile() -- set the global profiling function
    setrecursionlimit() -- set the max recursion depth for the interpreter
    settrace() -- set the global debug tracing function

内置模块内的函数、类以及方法在其 `__doc__` 属性内也有附加的说明信息。

```python
print(sys.getrefcount.__doc__)
```

    getrefcount(object) -> integer
    
    Return the reference count of object.  The count returned is generally
    one higher than you might expect, because it includes the (temporary)
    reference as an argument to getrefcount().

## 1.4 PyDoc：help 函数  
标准 PyDoc 工具是 Python 程序代码，知道如何提取文档字符串并且自动提取其结构化的信息，并将其格式化成各种类型的排列友好的列表。  

启动 PyDoc 有很多种方法，包括命令行脚本选项，可以将生成的文档保存到以后查看。两种最主要的 PyDoc 接口是内置的 help 函数和 PyDoc GUI/HTML 接口。

```python
import sys
help(sys.getrefcount)
```

    Help on built-in function getrefcount in module sys:
    
    getrefcount(...)
        getrefcount(object) -> integer
        
        Return the reference count of object.  The count returned is generally
        one higher than you might expect, because it includes the (temporary)
        reference as an argument to getrefcount().

调用 help 时，不一定要导入 sys，但是要取得 sys 的帮助信息时，就得导入 sys，help 需要有个对象的引用值传入。  

通过将引用模块名作为一个字符串，可以不导入模块来获得帮助，对于较大的对象，例如模块和类，help 显示内容会分成几段：

```python
help("re")
```

    Help on module re:
    
    NAME
        re - Support for regular expressions (RE).
    
    DESCRIPTION
        This module provides regular expression matching operations similar to
        those found in Perl.  It supports both 8-bit and Unicode strings; both
        the pattern and the strings being processed can contain null bytes and
        characters outside the US ASCII range.
        
        Regular expressions can contain both special and ordinary characters.
        Most ordinary characters, like "A", "a", or "0", are the simplest
        regular expressions; they simply match themselves.  You can
        concatenate ordinary characters, so last matches the string 'last'.
        
        The special characters are:
            "."      Matches any character except a newline.
            "^"      Matches the start of the string.
            "$"      Matches the end of the string or just before the newline at
                     the end of the string.
            "*"      Matches 0 or more (greedy) repetitions of the preceding RE.
                     Greedy means that it will match as many repetitions as possible.
            "+"      Matches 1 or more (greedy) repetitions of the preceding RE.
            "?"      Matches 0 or 1 (greedy) of the preceding RE.
            *?,+?,?? Non-greedy versions of the previous three special characters.
            {m,n}    Matches from m to n repetitions of the preceding RE.
            {m,n}?   Non-greedy version of the above.
            "\\"     Either escapes special characters or signals a special sequence.
            []       Indicates a set of characters.
                     A "^" as the first character indicates a complementing set.
            "|"      A|B, creates an RE that will match either A or B.
            (...)    Matches the RE inside the parentheses.
                     The contents can be retrieved or matched later in the string.
            (?aiLmsux) Set the A, I, L, M, S, U, or X flag for the RE (see below).
            (?:...)  Non-grouping version of regular parentheses.
            (?P<name>...) The substring matched by the group is accessible by name.
            (?P=name)     Matches the text matched earlier by the group named name.
            (?#...)  A comment; ignored.
            (?=...)  Matches if ... matches next, but doesn't consume the string.
            (?!...)  Matches if ... doesn't match next.
            (?<=...) Matches if preceded by ... (must be fixed length).
            (?<!...) Matches if not preceded by ... (must be fixed length).
            (?(id/name)yes|no) Matches yes pattern if the group with id/name matched,
                               the (optional) no pattern otherwise.
        
        The special sequences consist of "\\" and a character from the list
        below.  If the ordinary character is not on the list, then the
        resulting RE will match the second character.
            \number  Matches the contents of the group of the same number.
            \A       Matches only at the start of the string.
            \Z       Matches only at the end of the string.
            \b       Matches the empty string, but only at the start or end of a word.
            \B       Matches the empty string, but not at the start or end of a word.
            \d       Matches any decimal digit; equivalent to the set [0-9] in
                     bytes patterns or string patterns with the ASCII flag.
                     In string patterns without the ASCII flag, it will match the whole
                     range of Unicode digits.
            \D       Matches any non-digit character; equivalent to [^\d].
            \s       Matches any whitespace character; equivalent to [ \t\n\r\f\v] in
                     bytes patterns or string patterns with the ASCII flag.
                     In string patterns without the ASCII flag, it will match the whole
                     range of Unicode whitespace characters.
            \S       Matches any non-whitespace character; equivalent to [^\s].
            \w       Matches any alphanumeric character; equivalent to [a-zA-Z0-9_]
                     in bytes patterns or string patterns with the ASCII flag.
                     In string patterns without the ASCII flag, it will match the
                     range of Unicode alphanumeric characters (letters plus digits
                     plus underscore).
                     With LOCALE, it will match the set [0-9_] plus characters defined
                     as letters for the current locale.
            \W       Matches the complement of \w.
            \\       Matches a literal backslash.
        
        This module exports the following functions:
            match     Match a regular expression pattern to the beginning of a string.
            fullmatch Match a regular expression pattern to all of a string.
            search    Search a string for the presence of a pattern.
            sub       Substitute occurrences of a pattern found in a string.
            subn      Same as sub, but also return the number of substitutions made.
            split     Split a string by the occurrences of a pattern.
            findall   Find all occurrences of a pattern in a string.
            finditer  Return an iterator yielding a match object for each match.
            compile   Compile a pattern into a RegexObject.
            purge     Clear the regular expression cache.
            escape    Backslash all non-alphanumerics in a string.
        
        Some of the functions in this module takes flags as optional parameters:
            A  ASCII       For string patterns, make \w, \W, \b, \B, \d, \D
                           match the corresponding ASCII character categories
                           (rather than the whole Unicode categories, which is the
                           default).
                           For bytes patterns, this flag is the only available
                           behaviour and needn't be specified.
            I  IGNORECASE  Perform case-insensitive matching.
            L  LOCALE      Make \w, \W, \b, \B, dependent on the current locale.
            M  MULTILINE   "^" matches the beginning of lines (after a newline)
                           as well as the string.
                           "$" matches the end of lines (before a newline) as well
                           as the end of the string.
            S  DOTALL      "." matches any character at all, including the newline.
            X  VERBOSE     Ignore whitespace and comments for nicer looking RE's.
            U  UNICODE     For compatibility only. Ignored for string patterns (it
                           is the default), and forbidden for bytes patterns.
        
        This module also defines an exception 'error'.
    
    CLASSES
        builtins.Exception(builtins.BaseException)
            sre_constants.error
        
        class error(builtins.Exception)
         |  Exception raised for invalid regular expressions.
         |  
         |  Attributes:
         |  
         |      msg: The unformatted error message
         |      pattern: The regular expression pattern
         |      pos: The index in the pattern where compilation failed (may be None)
         |      lineno: The line corresponding to pos (may be None)
         |      colno: The column corresponding to pos (may be None)
         |  
         |  Method resolution order:
         |      error
         |      builtins.Exception
         |      builtins.BaseException
         |      builtins.object
         |  
         |  Methods defined here:
         |  
         |  __init__(self, msg, pattern=None, pos=None)
         |      Initialize self.  See help(type(self)) for accurate signature.
         |  
         |  ----------------------------------------------------------------------
         |  Data descriptors defined here:
         |  
         |  __weakref__
         |      list of weak references to the object (if defined)
         |  
         |  ----------------------------------------------------------------------
         |  Methods inherited from builtins.Exception:
         |  
         |  __new__(*args, **kwargs) from builtins.type
         |      Create and return a new object.  See help(type) for accurate signature.
         |  
         |  ----------------------------------------------------------------------
         |  Methods inherited from builtins.BaseException:
         |  
         |  __delattr__(self, name, /)
         |      Implement delattr(self, name).
         |  
         |  __getattribute__(self, name, /)
         |      Return getattr(self, name).
         |  
         |  __reduce__(...)
         |      helper for pickle
         |  
         |  __repr__(self, /)
         |      Return repr(self).
         |  
         |  __setattr__(self, name, value, /)
         |      Implement setattr(self, name, value).
         |  
         |  __setstate__(...)
         |  
         |  __str__(self, /)
         |      Return str(self).
         |  
         |  with_traceback(...)
         |      Exception.with_traceback(tb) --
         |      set self.__traceback__ to tb and return self.
         |  
         |  ----------------------------------------------------------------------
         |  Data descriptors inherited from builtins.BaseException:
         |  
         |  __cause__
         |      exception cause
         |  
         |  __context__
         |      exception context
         |  
         |  __dict__
         |  
         |  __suppress_context__
         |  
         |  __traceback__
         |  
         |  args
    
    FUNCTIONS
        compile(pattern, flags=0)
            Compile a regular expression pattern, returning a pattern object.
        
        escape(pattern)
            Escape all the characters in pattern except ASCII letters, numbers and '_'.
        
        findall(pattern, string, flags=0)
            Return a list of all non-overlapping matches in the string.
            
            If one or more capturing groups are present in the pattern, return
            a list of groups; this will be a list of tuples if the pattern
            has more than one group.
            
            Empty matches are included in the result.
        
        finditer(pattern, string, flags=0)
            Return an iterator over all non-overlapping matches in the
            string.  For each match, the iterator returns a match object.
            
            Empty matches are included in the result.
        
        fullmatch(pattern, string, flags=0)
            Try to apply the pattern to all of the string, returning
            a match object, or None if no match was found.
        
        match(pattern, string, flags=0)
            Try to apply the pattern at the start of the string, returning
            a match object, or None if no match was found.
        
        purge()
            Clear the regular expression caches
        
        search(pattern, string, flags=0)
            Scan through string looking for a match to the pattern, returning
            a match object, or None if no match was found.
        
        split(pattern, string, maxsplit=0, flags=0)
            Split the source string by the occurrences of the pattern,
            returning a list containing the resulting substrings.  If
            capturing parentheses are used in pattern, then the text of all
            groups in the pattern are also returned as part of the resulting
            list.  If maxsplit is nonzero, at most maxsplit splits occur,
            and the remainder of the string is returned as the final element
            of the list.
        
        sub(pattern, repl, string, count=0, flags=0)
            Return the string obtained by replacing the leftmost
            non-overlapping occurrences of the pattern in string by the
            replacement repl.  repl can be either a string or a callable;
            if a string, backslash escapes in it are processed.  If it is
            a callable, it's passed the match object and must return
            a replacement string to be used.
        
        subn(pattern, repl, string, count=0, flags=0)
            Return a 2-tuple containing (new_string, number).
            new_string is the string obtained by replacing the leftmost
            non-overlapping occurrences of the pattern in the source
            string by the replacement repl.  number is the number of
            substitutions that were made. repl can be either a string or a
            callable; if a string, backslash escapes in it are processed.
            If it is a callable, it's passed the match object and must
            return a replacement string to be used.
        
        template(pattern, flags=0)
            Compile a template pattern, returning a pattern object
    
    DATA
        A = <RegexFlag.ASCII: 256>
        ASCII = <RegexFlag.ASCII: 256>
        DOTALL = <RegexFlag.DOTALL: 16>
        I = <RegexFlag.IGNORECASE: 2>
        IGNORECASE = <RegexFlag.IGNORECASE: 2>
        L = <RegexFlag.LOCALE: 4>
        LOCALE = <RegexFlag.LOCALE: 4>
        M = <RegexFlag.MULTILINE: 8>
        MULTILINE = <RegexFlag.MULTILINE: 8>
        S = <RegexFlag.DOTALL: 16>
        U = <RegexFlag.UNICODE: 32>
        UNICODE = <RegexFlag.UNICODE: 32>
        VERBOSE = <RegexFlag.VERBOSE: 64>
        X = <RegexFlag.VERBOSE: 64>
        __all__ = ['match', 'fullmatch', 'search', 'sub', 'subn', 'split', 'fi...
    
    VERSION
        2.2.1
    
    FILE
        e:\anaconda\lib\re.py

也可以对内置函数、方法以及类型使用 help：

```python
help(dict)
```

    Help on class dict in module builtins:
    
    class dict(object)
     |  dict() -> new empty dictionary
     |  dict(mapping) -> new dictionary initialized from a mapping object's
     |      (key, value) pairs
     |  dict(iterable) -> new dictionary initialized as if via:
     |      d = {}
     |      for k, v in iterable:
     |          d[k] = v
     |  dict(**kwargs) -> new dictionary initialized with the name=value pairs
     |      in the keyword argument list.  For example:  dict(one=1, two=2)
     |  
     |  Methods defined here:
     |  
     |  __contains__(self, key, /)
     |      True if D has a key k, else False.
     |  
     |  __delitem__(self, key, /)
     |      Delete self[key].
     |  
     |  __eq__(self, value, /)
     |      Return self==value.
     |  
     |  __ge__(self, value, /)
     |      Return self>=value.
     |  
     |  __getattribute__(self, name, /)
     |      Return getattr(self, name).
     |  
     |  __getitem__(...)
     |      x.__getitem__(y) <==> x[y]
     |  
     |  __gt__(self, value, /)
     |      Return self>value.
     |  
     |  __init__(self, /, *args, **kwargs)
     |      Initialize self.  See help(type(self)) for accurate signature.
     |  
     |  __iter__(self, /)
     |      Implement iter(self).
     |  
     |  __le__(self, value, /)
     |      Return self<=value.
     |  
     |  __len__(self, /)
     |      Return len(self).
     |  
     |  __lt__(self, value, /)
     |      Return self<value.
     |  
     |  __ne__(self, value, /)
     |      Return self!=value.
     |  
     |  __new__(*args, **kwargs) from builtins.type
     |      Create and return a new object.  See help(type) for accurate signature.
     |  
     |  __repr__(self, /)
     |      Return repr(self).
     |  
     |  __setitem__(self, key, value, /)
     |      Set self[key] to value.
     |  
     |  __sizeof__(...)
     |      D.__sizeof__() -> size of D in memory, in bytes
     |  
     |  clear(...)
     |      D.clear() -> None.  Remove all items from D.
     |  
     |  copy(...)
     |      D.copy() -> a shallow copy of D
     |  
     |  fromkeys(iterable, value=None, /) from builtins.type
     |      Returns a new dict with keys from iterable and values equal to value.
     |  
     |  get(...)
     |      D.get(k[,d]) -> D[k] if k in D, else d.  d defaults to None.
     |  
     |  items(...)
     |      D.items() -> a set-like object providing a view on D's items
     |  
     |  keys(...)
     |      D.keys() -> a set-like object providing a view on D's keys
     |  
     |  pop(...)
     |      D.pop(k[,d]) -> v, remove specified key and return the corresponding value.
     |      If key is not found, d is returned if given, otherwise KeyError is raised
     |  
     |  popitem(...)
     |      D.popitem() -> (k, v), remove and return some (key, value) pair as a
     |      2-tuple; but raise KeyError if D is empty.
     |  
     |  setdefault(...)
     |      D.setdefault(k[,d]) -> D.get(k,d), also set D[k]=d if k not in D
     |  
     |  update(...)
     |      D.update([E, ]**F) -> None.  Update D from dict/iterable E and F.
     |      If E is present and has a .keys() method, then does:  for k in E: D[k] = E[k]
     |      If E is present and lacks a .keys() method, then does:  for k, v in E: D[k] = v
     |      In either case, this is followed by: for k in F:  D[k] = F[k]
     |  
     |  values(...)
     |      D.values() -> an object providing a view on D's values
     |  
     |  ----------------------------------------------------------------------
     |  Data and other attributes defined here:
     |  
     |  __hash__ = None

```python
help(str.replace)
```

    Help on method_descriptor:
    
    replace(...)
        S.replace(old, new[, count]) -> str
        
        Return a copy of S with all occurrences of substring
        old replaced by new.  If the optional argument count is
        given, only the first count occurrences are replaced.

help 函数也能用在模块上，就像内置工具一样。

```python
import docstring
help(docstring.square)
```

    Help on function square in module docstring:
    
    square(x)
        function documentation
        can we have your liver then?

```python
help(docstring.Employee)
```

    Help on class Employee in module docstring:
    
    class Employee(builtins.object)
     |  class documentation
     |  
     |  Data descriptors defined here:
     |  
     |  __dict__
     |      dictionary for instance variables (if defined)
     |  
     |  __weakref__
     |      list of weak references to the object (if defined)

```python
help(docstring)
```

    Help on module docstring:
    
    NAME
        docstring
    
    DESCRIPTION
        Module documentation
        Words Go Here
    
    CLASSES
        builtins.object
            Employee
        
        class Employee(builtins.object)
         |  class documentation
         |  
         |  Data descriptors defined here:
         |  
         |  __dict__
         |      dictionary for instance variables (if defined)
         |  
         |  __weakref__
         |      list of weak references to the object (if defined)
    
    FUNCTIONS
        square(x)
            function documentation
            can we have your liver then?
    
    DATA
        spam = 40
    
    FILE
        c:\users\lan\desktop\python\python-note\learning python\三、语句和语法\docstring.py

## 1.5 PyDoc：HTML  报表  
在许多环境中，特别是在交互提示符下，help 函数的文本显示是足够的。对于那些已经习惯了更丰富的展示的读者来说，它们可能看起来有点原始。  

基于 HTML 的 PyDoc 以图形化方式呈现模块文档，以便在 web 浏览器中查看，甚至可以自动打开模块文档。  

**Python 3.2 之后的版本**  
在 Python 3.3 中，PyDoc 的原始 GUI 客户端模式不再可用，取而代之的是 pydoc -b 命令行，它生成本地运行的文档服务器，以及同时作为搜索引擎客户端和页面显示的 web 浏览器。  

还有其他方法可以使用 PyDoc(例如，将 HTML 页面保存到文件中，以供以后查看)。  

使用 -m Python 命令行参数来方便地在模块导入搜索路径上定位 PyDoc 的模块文件。

```python
!python -m pydoc -b               # 该命令假设 Python 在系统路径上
```

```python
!py -3 -m pydoc -b                # 该命令假设采用 Python 3.3 的新 Windows 启动程序
```

```python
!C:\python3\python -m pydoc -b    # 该命令使用完整 Python 路径
```

无论你怎么运行这个命令行，效果都是启动 PyDoc 作为本地运行的 web 服务器，且运行在一个专用的端口上，并弹出一个网页浏览器作为客户端，显示所有在模块搜索路径上可导入的模块。  

除了模块索引之外，PyDoc 的 web 页面还在顶部包含输入字段，以请求特定模块的文档页面和搜索相关条目，后者代表先前接口的 GUI 客户端字段。  

Python 3.3 中的 PyDoc 还支持其他以前的使用模式。例如，`pydoc -p port` 可以用来设置 pydoc 服务器端口；`pydoc -w module` 仍然将模块的 HTML 文档写入到一个名为 module.html 的文件中供以后查看；只有 `pydoc -g` GUI 客户端模式被删除并由 `pydoc -b` 替换。你还可以运行 PyDoc 来生成文档的明文形式(本章前面显示的Unix“manpage”风格)——以下命令行相当于交互式 Python 提示符的 help 调用:

```python
!py -3 -m pydoc timeit
```

```python
!python
```

```python
help('timeit')
```

## 1.6 不止文档字符串：Sphinx  
如果你正在寻找一种以更精密的方式记录 Python 系统的方法，你可能希望查看 Sphinx（ http://sphinx-doc.org ）。Sphinx 由标准 Python 文档和许多其他项目使用。它使用简单的 reStructuredText 作为标记语言，并从 reStructuredText 解析和翻译工具的 Docutils 套件中继承了许多内容。  

Sphinx 支持多种输出格式(包括 Windows HTML 帮助、可打印 PDF 版本的 LaTeX、手册和纯文本)；广泛而自动的交叉引用；层次化结构，与相关项自动链接；自动索引；使用 Pygments 自动突出显示代码等等。对于小型的程序来说，docstring 和 PyDoc 可能已经足够了，但是对于大型项目来说，它们可以生成专业级的文档。  

# 2. 常见编写代码的陷阱  
- **别忘了冒号。**
- **从第一列开始。**
- **空白行在交互模式提示符下很重要。**模块文件中复合语句内的空白行都会被忽略，但在交互模式提示符下的空白行则会结束语句。
- **缩进要一致。**避免在块缩进中混合制表符和空格。
- **不要在 Python 中写 C 代码。**
- **使用简单的 for 循环，而不是 while 或 range。**
- **要注意赋值语句中的可变对象。**
- **不要期待在原处修改对象的函数会返回结果。**
- **一定要使用括号调用函数。**
- **不要在导入和重载中使用扩展名或路径。**在 import 语句中省略目录路径和文件扩展名，要写 import mod，而不是 import mod.py。

```python

```
