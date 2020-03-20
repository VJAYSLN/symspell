## Symspell

## How to install this

??? I tried `cd` ing in and `pip install .`

But I get:

```sh
Processing /app/symspell/bindings/Python
  Installing build dependencies ... done
  Getting requirements to build wheel ... done
    Preparing wheel metadata ... done
Building wheels for collected packages: symspell-rs
  Building wheel for symspell-rs (PEP 517) ... error
  ERROR: Command errored out with exit status 1:
   command: /usr/local/bin/python /usr/local/lib/python3.7/site-packages/pip/_vendor/pep517/_in_process.py build_wheel /tmp/tmpkoqg_wpn
       cwd: /tmp/pip-req-build-raxa8_n5
  Complete output (70 lines):
  running bdist_wheel
  running build
  running build_py
  creating build
  creating build/lib
  creating build/lib/symspell_rs
  copying symspell_rs/__init__.py -> build/lib/symspell_rs
  running build_ext
  running build_rust
  error: failed to get `symspell` as a dependency of package `symspell_rs v0.3.0 (/tmp/pip-req-build-raxa8_n5)`

  Caused by:
    failed to load source for dependency `symspell`

  Caused by:
    Unable to update /

  Caused by:
    failed to read `/Cargo.toml`

  Caused by:
    No such file or directory (os error 2)
  Traceback (most recent call last):
    File "/usr/local/lib/python3.7/site-packages/pip/_vendor/pep517/_in_process.py", line 257, in <module>
      main()
    File "/usr/local/lib/python3.7/site-packages/pip/_vendor/pep517/_in_process.py", line 240, in main
      json_out['return_val'] = hook(**hook_input['kwargs'])
    File "/usr/local/lib/python3.7/site-packages/pip/_vendor/pep517/_in_process.py", line 182, in build_wheel
      metadata_directory)
    File "/tmp/pip-build-env-t_titx6a/overlay/lib/python3.7/site-packages/setuptools/build_meta.py", line 213, in build_wheel
      wheel_directory, config_settings)
    File "/tmp/pip-build-env-t_titx6a/overlay/lib/python3.7/site-packages/setuptools/build_meta.py", line 198, in _build_with_temp_dir
      self.run_setup()
    File "/tmp/pip-build-env-t_titx6a/overlay/lib/python3.7/site-packages/setuptools/build_meta.py", line 250, in run_setup
      self).run_setup(setup_script=setup_script)
    File "/tmp/pip-build-env-t_titx6a/overlay/lib/python3.7/site-packages/setuptools/build_meta.py", line 143, in run_setup
      exec(compile(code, __file__, 'exec'), locals())
    File "setup.py", line 16, in <module>
      zip_safe=False,
    File "/tmp/pip-build-env-t_titx6a/overlay/lib/python3.7/site-packages/setuptools/__init__.py", line 144, in setup
      return distutils.core.setup(**attrs)
    File "/usr/local/lib/python3.7/distutils/core.py", line 148, in setup
      dist.run_commands()
    File "/usr/local/lib/python3.7/distutils/dist.py", line 966, in run_commands
      self.run_command(cmd)
    File "/usr/local/lib/python3.7/distutils/dist.py", line 985, in run_command
      cmd_obj.run()
    File "/tmp/pip-build-env-t_titx6a/overlay/lib/python3.7/site-packages/wheel/bdist_wheel.py", line 223, in run
      self.run_command('build')
    File "/usr/local/lib/python3.7/distutils/cmd.py", line 313, in run_command
      self.distribution.run_command(command)
    File "/usr/local/lib/python3.7/distutils/dist.py", line 985, in run_command
      cmd_obj.run()
    File "/usr/local/lib/python3.7/distutils/command/build.py", line 135, in run
      self.run_command(cmd_name)
    File "/usr/local/lib/python3.7/distutils/cmd.py", line 313, in run_command
      self.distribution.run_command(command)
    File "/usr/local/lib/python3.7/distutils/dist.py", line 985, in run_command
      cmd_obj.run()
    File "/tmp/pip-build-env-t_titx6a/overlay/lib/python3.7/site-packages/setuptools_rust/build_ext.py", line 26, in run
      build_rust.run()
    File "/tmp/pip-build-env-t_titx6a/overlay/lib/python3.7/site-packages/setuptools_rust/build.py", line 313, in run
      self.build_extension(ext)
    File "/tmp/pip-build-env-t_titx6a/overlay/lib/python3.7/site-packages/setuptools_rust/build.py", line 95, in build_extension
      metadata = json.loads(check_output(metadata_command).decode("utf-8"))
    File "/usr/local/lib/python3.7/subprocess.py", line 411, in check_output
      **kwargs).stdout
    File "/usr/local/lib/python3.7/subprocess.py", line 512, in run
      output=stdout, stderr=stderr)
  subprocess.CalledProcessError: Command '['cargo', 'metadata', '--manifest-path', 'Cargo.toml', '--format-version', '1']' returned non-zero exit status 101.
  ----------------------------------------
  ERROR: Failed building wheel for symspell-rs
Failed to build symspell-rs
ERROR: Could not build wheels for symspell-rs which use PEP 517 and cannot be installed directly
```

This happens even though `cargo build` works. Any advice?

## Quick examples using Python:

```python
>>> from symspell_rs import SymspellPy
>>> sym_spell = SymspellPy(max_distance=2,prefix_length=7,count_threshold=1)
>>> if not sym_spell.load_dictionary("./data/frequency_dictionary_en_82_765.txt",0,1," "):
      print("File Not Found")
>>> suggestions = sym_spell.lookup_compound("whereis th elove hehad dated forImuch of thepast who couqdn'tread in sixtgrade and ins pired him",2)
>>> for cand in suggestions:
    print(f"Term->{cand.term} \n Distance->{cand.distance} \n Count->{cand.count}")
>>> segment_obj = sym_spell.word_segmentation("whereisthelove",2)
>>> print(f"String->{segment_obj.segmented_string} \n Distance->{segment_obj.distance_sum} \n Prob_Log_Sum->{segment_obj.prob_log_sum}")
```
