---
layout: ../../layouts/ProjectLayout.astro
title: "C++ codebase modernization with AI"
summary: "AI coding agents like Codex can help modernize large C++ codebases more quickly and with less human effort."
author: "Arnaud de Grandmaison"
---

## Challenge

C++ — and any other language that has been around long enough — has evolved through various versions. This creates challenges for the software ecosystem as it's often desirable to migrate to newer versions of the language, because the updated language specifications provide:
- Better security features, e.g., smart pointers to prevent memory safety issues.
- Performance improvements, e.g., move semantics.
- Better expressiveness, allowing you to remove code duplication, e.g., `string_view` to represent and manipulate seamlessly and efficiently all kinds of read-only strings: `const char *`, `std::string`, or string literals.

Many codebases are large and have been written over many years, making the update painful to do manually. Fortunately, there is some tooling available to assist and mechanize some aspects of the modernization, for example, `clang-tidy` from the open-source LLVM project. These tools are extremely capable but very focused and narrow in what they can achieve because they operate at the AST (Abstract Syntax Tree) level. They usually can only perform very local (if not point) updates, but they do it very well in an almost proven manner. The challenge is that many updates require a wider view of the codebase.

## Solution

OpenAI has published an AI coding agent named [Codex CLI](https://github.com/openai/codex), an open-source local coding agent.

## AI developer tools used

- OpenAI Codex

## Results

I applied Codex CLI to a codebase of about 35k lines of C++.

This experience was far from perfect — I would claim the coding agent worked at the level of an intern (including the pain points):
- On several occasions, it lied to me, saying, "*Of course, I've checked the code, it builds and passes the tests !*"
- Messed up the codebase by using `git` in weird ways.
- Modified the code in ways that obviously cannot compile, e.g., unmatched parentheses.
- Duplicated comments.
- ...

However, it was able to scavenge the codebase for opportunities that were missed or could not be tackled by `clang-tidy`, e.g. migrating to `string_view`. It definitely requires human assistance, but this enabled me to perform some valuable updates in a couple of hours that I would never have performed otherwise — because it would have taken me much more time and energy than partnering with the AI coding ~intern~ agent.
