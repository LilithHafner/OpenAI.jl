
# OpenAI API wrapper for Julia (Unofficial)

[![Stable](https://img.shields.io/badge/docs-stable-blue.svg)](https://juliaml.github.io/OpenAI.jl/stable/)
[![In Development](https://img.shields.io/badge/docs-dev-blue.svg)](https://juliaml.github.io/OpenAI.jl/dev/)

## Overview

Provides a community maintained Julia wrapper to the OpenAI API.
For API functionality see [reference documentation](https://platform.openai.com/docs/api-reference).
Autogenerated documentation can be found here: https://juliaml.github.io/OpenAI.jl/dev/

## Usage

```julia
using Pkg; Pkg.add("OpenAI")
```

## Quick Start

1. Create an [OpenAI account](https://chat.openai.com/auth/login), if you don't already have one

2. Create a [secret API key](https://platform.openai.com/account/api-keys)

3. Choose a [model](https://platform.openai.com/docs/models) to interact with

__⚠️ We strongly suggest setting up your API key as an ENV variable__.

```julia
secret_key = ENV["OPENAI_API_KEY"]
model = "gpt-4o-mini"
prompt =  "Say \"this is a test\""

r = create_chat(
    secret_key,
    model,
    [Dict("role" => "user", "content"=> prompt)]
  )
println(r.response[:choices][begin][:message][:content])
```
returns
```julia
"This is a test."
```

### Overriding default parameters

If you have a non-standard setup, such as a local LLM or third-party service that
conforms to the OpenAI interface, you can override parameters using the `OpenAIProvider`
struct in your application like this:

```julia
using OpenAI
provider = OpenAI.OpenAIProvider(
    api_key=ENV["OPENAI_API_KEY"],
    base_url=ENV["OPENAI_BASE_URL_OVERRIDE"]
)
response = create_chat(
    provider,
    "gpt-4o-mini",
    [Dict("role" => "user", "content" => "Write some ancient Greek poetry")]
)
```

For more use cases [see tests](https://github.com/JuliaML/OpenAI.jl/tree/main/test).

## Feature requests

Feel free to open a PR, or file an issue if that's out of reach!
