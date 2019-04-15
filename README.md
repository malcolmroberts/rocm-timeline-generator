# rocm-timeline-generator

This page explains how to generate a single timeline that shows HIP
and HCC events.

There are three steps to do it:

1. Run your program with appropriate profiling flags and capture the log

2. Format your log using the rocm-timeline-generator.sh script and
create a json file for viewing

3. Visualize your timeline in chrome://tracing/

### 1. Profile your program

The timeline generating tool can be used to display HIP or HCC
timeline or both based on the environment variables set to gather
events log during the application run.

* To obtain HCC trace, use env variables:
    HCC_PROFILE=2 HCC_PROFILE_VERBOSE=0x1f
  
* To obtain HIP trace, use env variables
    HIP_TRACE_API=1 HIP_TRACE_API_COLOR=none
    
You may choose to enable one or both HIP or HCC trace to capture the log.  

**Example 1: HCC log**  
HCC_PROFILE=2 HCC_PROFILE_VERBOSE=0x1f python test.py 2>&1 | tee log

**Example 2: HIP and HCC log**  

HIP_TRACE_API=1 HIP_TRACE_API_COLOR=none HCC_PROFILE=2 HCC_PROFILE_VERBOSE=0x1f python test.py 2>&1 | tee log

### 2. Formatting the log, creating a json file

Format the log files obtained from step.1 using the
rocm-timeline-generator.sh to create a json file to be viewed using
chrome://tracing/

Syntax:  `rocm-timeline-generator.sh <input log file> <output json filename>`  
For example: `rocm-timeline-generator.sh log test_profile.json`

### 3. Visualize the timeline

You can open the json file using chrome://tracing/. You can zoom into
the timeline and it displays the HCC kernel name overlaid on the time
bar associated with that kernel execution
