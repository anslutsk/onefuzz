# Commandline Injection

The following values are replaced with the specific values at runtime.

* `{input}`: Path to the input file being processed in the current event
* `{crashes}`: Path to write crashes
* `{input_corpus}`: Path to the input corpus directory
* `{generated_inputs}`: Path to the generated inputs directory
* `{target_exe}`: Path to the target binary
* `{target_options}`: Target options (recursively expanded)
* `{output_dir}` : Path to the output directory as defined by the task
* `{input_file_name}`: the input file name with the extension (available
  wherever `input` is available)
* `{input_file_name_no_ext}`: the input file name without the extension
  (available wherever `input` is available)
* `{runtime_dir}`: Path to the runtime directory for the task
* `{tools_dir}`: Path to the task specific `tools` directory
* `{setup_dir}` : Path to the setup directory
* `{job_id}`: UUID that indicates the Job ID
* `{task_id}`: UUID that indicates the Task ID

## Example

Assume the following:

* `supervisor_options` is: ``"a", "{target_options}", "d"`
* `target_options` is: `"b", "{target_exe}"`
* `target_exe` is: `"c"`

The resulting `supervisor_options` is: `"a", "b c", "d"`.

If you need `supervisor_options` to expand to: `"a", "b", "c", "d"`, you should use the following values:

* `supervisor_options`: `"a", "b", "{target_exe}", "d"`
* `target_options`: `"b", "{target_exe}"`
* `target_exe`: `"c"`


## Uses

These are currently used in the following tasks:

* libfuzzer\_fuzz: `target_exe`, `target_options`, `input_corpus`, `crashes`
* libfuzzer\_crash\_report: `target_exe`, `target_options`, `input`
* libfuzzer\_merge: `target_exe`, `target_options`, `input_corpus`
* libfuzzer\_coverage: None
* generic\_analysis: `input`, `target_exe`, `target_options`, `analyzer_exe`,
  `anayzer_options`, `output_dir`, `tools_dir`, `job_id`, `task_id`
* generic\_generator: `generated_inputs`, `input_corpus`, `tools_dir`,
  `generator_exe`, `generator_options`, `target_exe`, `target_options`,
  `input`, `job_id`, `task_id`
* generic\_supervisor: `crashes`, `runtime_dir`, `target_exe`, `target_options`,
  `input_corpus`, `input`, `supervisor_exe`, `supervisor_options`, `tools_dir`,
  `job_id`, `task_id`
* generic\_merge: `input`, `input_corpus`, `output_dir`, `target_exe`,
  `target_options`, `supervisor_exe`, `supervisor_options`, `tools_dir`,
  `job_id`, `task_id`
