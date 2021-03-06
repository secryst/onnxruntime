# ONNX Runtime

:fire: [ONNX Runtime](https://github.com/Microsoft/onnxruntime) - the high performance scoring engine for ML models - for Ruby

Check out [an example](https://ankane.org/tensorflow-ruby)

[![Build Status](https://github.com/ankane/onnxruntime/workflows/build/badge.svg?branch=master)](https://github.com/ankane/onnxruntime/actions)

## Installation

Add this line to your application’s Gemfile:

```ruby
gem 'onnxruntime'
```

On Mac, also install OpenMP:

```sh
brew install libomp
```

## Getting Started

Load a model and make predictions

```ruby
model = OnnxRuntime::Model.new("model.onnx")
model.predict({x: [1, 2, 3]})
```

> Download pre-trained models from the [ONNX Model Zoo](https://github.com/onnx/models)

Get inputs

```ruby
model.inputs
```

Get outputs

```ruby
model.outputs
```

Get metadata

```ruby
model.metadata
```

Load a model from a string

```ruby
byte_str = StringIO.new("...")
model = OnnxRuntime::Model.new(byte_str)
```

Get specific outputs

```ruby
model.predict({x: [1, 2, 3]}, output_names: ["label"])
```

## Session Options

```ruby
OnnxRuntime::Model.new(path_or_bytes, {
  enable_cpu_mem_arena: true,
  enable_mem_pattern: true,
  enable_profiling: false,
  execution_mode: :sequential,    # :sequential or :parallel
  graph_optimization_level: nil,  # :none, :basic, :extended, or :all
  inter_op_num_threads: nil,
  intra_op_num_threads: nil,
  log_severity_level: 2,
  log_verbosity_level: 0,
  logid: nil,
  optimized_model_filepath: nil
})
```

## Run Options

```ruby
model.predict(input_feed, {
  log_severity_level: 2,
  log_verbosity_level: 0,
  logid: nil,
  terminate: false,
  output_type: :ruby       # :ruby or :numo
})
```

## Inference Session API

You can also use the Inference Session API, which follows the [Python API](https://microsoft.github.io/onnxruntime/python/api_summary.html).

```ruby
session = OnnxRuntime::InferenceSession.new("model.onnx")
session.run(nil, {x: [1, 2, 3]})
```

The Python example models are included as well.

```ruby
OnnxRuntime::Datasets.example("sigmoid.onnx")
```

## GPU Support

To enable GPU support on Linux and Windows, download the appropriate [GPU release](https://github.com/microsoft/onnxruntime/releases) and set:

```ruby
OnnxRuntime.ffi_lib = "path/to/lib/libonnxruntime.so" # onnxruntime.dll for Windows
```

## History

View the [changelog](https://github.com/ankane/onnxruntime/blob/master/CHANGELOG.md)

## Contributing

Everyone is encouraged to help improve this project. Here are a few ways you can help:

- [Report bugs](https://github.com/ankane/onnxruntime/issues)
- Fix bugs and [submit pull requests](https://github.com/ankane/onnxruntime/pulls)
- Write, clarify, or fix documentation
- Suggest or add new features

To get started with development and testing:

```sh
git clone https://github.com/ankane/onnxruntime.git
cd onnxruntime
bundle install
bundle exec rake vendor:all
bundle exec rake test
```
