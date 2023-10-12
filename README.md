# Rust-minigrep

## Explain main.rs code

这段代码是一个简单的命令行工具，用于在文件中搜索指定的字符串。以下是代码的步骤解释：

1. 导入了  `minigrep::Config`  结构体，该结构体用于存储程序的配置信息。
2. 导入了  `std::env`  和  `std::process`  模块，用于处理命令行参数和进程控制。
3. 在  `main`  函数中，通过调用  `Config::new`  方法创建了一个  `config`  对象，并将命令行参数传递给该方法。
4. 如果  `Config::new`  方法返回一个错误（表示参数解析失败），则使用  `eprintln!`  宏打印错误信息，并调用  `process::exit`  方法退出程序。
5. 如果参数解析成功，调用  `minigrep::run`  方法并将  `config`  对象作为参数传递给该方法。
6. 如果  `minigrep::run`  方法返回一个错误，表示搜索过程中发生了错误，同样使用  `eprintln!`  宏打印错误信息，并调用  `process::exit`  方法退出程序。

总结：该代码是一个简单的命令行工具，用于在文件中搜索指定的字符串。它通过  `Config`  结构体存储配置信息，并使用  `minigrep::run`  方法执行搜索操作。如果参数解析或搜索过程中发生错误，程序会打印错误信息并退出。

## Explain lib.rs code

这段代码是一个简单的文本搜索程序。它接受一个包含查询字符串和文件名的配置，并根据配置搜索文件中包含查询字符串的行。它可以根据配置的大小写敏感性进行搜索。

代码的步骤如下：

1. 导入必要的模块： `std::env` 用于处理命令行参数， `std::error::Error` 用于处理错误， `std::fs` 用于读取文件内容。
2. 定义一个名为 `run` 的函数，它接受一个 `Config` 结构体作为参数，并返回一个 `Result` 类型的结果。
3. 在 `run` 函数中，使用 `fs::read_to_string` 函数读取配置中指定的文件内容，并将结果存储在 `contents` 变量中。
4. 根据配置的大小写敏感性，使用 `search` 函数或 `search_case_insensitive` 函数对文件内容进行搜索，并将结果存储在 `results` 变量中。
5. 遍历 `results` 中的每一行，并打印出来。
6. 最后返回一个 `Ok(())` 表示函数执行成功。

 `Config` 结构体定义了查询字符串、文件名和大小写敏感性的字段，并提供了一个 `new` 方法来创建 `Config` 实例。 `new` 方法接受一个 `std::env::Args` 迭代器作为参数，从迭代器中获取查询字符串和文件名，并根据环境变量 `CASE_INSENSITIVE` 的值确定大小写敏感性。

 `search` 函数接受一个查询字符串和一个文本内容字符串作为参数，并返回一个包含匹配查询字符串的行的字符串切片的向量。它使用 `contents.lines()` 方法将文本内容按行分割，并使用 `filter` 方法过滤出包含查询字符串的行。

 `search_case_insensitive` 函数与 `search` 函数类似，但它会将查询字符串和文本内容都转换为小写字母后再进行匹配，以实现大小写不敏感的搜索。

 `tests` 模块包含了一些单元测试，用于测试 `search` 和 `search_case_insensitive` 函数的功能。其中 `case_sensitive` 函数测试了大小写敏感的搜索， `case_insensitive` 函数测试了大小写不敏感的搜索。

## Usage

```shell
minigrep on  master [?] is 📦 0.1.0 via 🦀 1.72.1 via 🅒 base 
➜ cargo run > output.txt    
   Compiling minigrep v0.1.0 (/Users/qiaopengjun/Code/rust/minigrep)
    Finished dev [unoptimized + debuginfo] target(s) in 0.94s
     Running `target/debug/minigrep`
Problem parsing arguments: not enough arguments

minigrep on  master [?] is 📦 0.1.0 via 🦀 1.72.1 via 🅒 base 
➜ cargo run -- to poem.txt > output.txt 
    Finished dev [unoptimized + debuginfo] target(s) in 0.02s
     Running `target/debug/minigrep to poem.txt`
```

更多详情请参考：<https://course.rs/basic-practice/intro.html#%E6%9E%84%E5%BB%BA%E4%B8%80%E4%B8%AA%E7%AE%80%E5%8D%95%E5%91%BD%E4%BB%A4%E8%A1%8C%E7%A8%8B%E5%BA%8F>
