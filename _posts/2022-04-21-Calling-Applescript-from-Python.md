---
layout: post
title: Calling Applescript from Python and passing in Variables
---

For work I had to automate a piece of software - which was seemingly best done with Applescript - but I wanted to be able to call on the script from Python and also pass in some variables. [py-applescript](https://github.com/rdhyee/py-applescript) seemed to be the best package to interface with Applescript and has examples of how to either a) call an external Applescript or b) pass in arguments. The documentation was a little less clear on how to do both at the same time. I eventually got everything working with code similar to what is below. You send the path of the external script to the AppleScript `class` (?) as a keyword argument (`"path=path_to_file.scpt"`) and the arguments to the `run` method (?).

```python
import applescript


APPLESCRIPT_LOCATION = "software_automation.scpt"

INPUT_LIST = ["/Users/User1/Downloads/input1"]
OUTPUT_LIST = [
    "/Users/User1/Downloads/output1",
    "/Users/User1/Downloads/output2",
    "/Users/User1/Downloads/output3",
]

CLIENT_NAME = "Client Name1"
PROJECT_NAME = "Project Name1"
JOB_NAME = "Job Name1"

EMAIL_ADDRESSES = "user@example.com"
REPORTS_DESTINATION = "/Users/User1/Downloads/1"


def software_automation(
    input_list,
    output_list,
    client_name,
    project_name,
    job_name,
    email_addresses,
    reports_destination,
):
    applescript.AppleScript(path=APPLESCRIPT_LOCATION).run(
        input_list,
        output_list,
        client_name,
        project_name,
        job_name,
        email_addresses,
        reports_destination,
    )


software_automation(
    input_list=INPUT_LIST,
    output_list=OUTPUT_LIST,
    client_name=CLIENT_NAME,
    project_name=PROJECT_NAME,
    job_name=JOB_NAME,
    email_addresses=EMAIL_ADDRESSES,
    reports_destination=REPORTS_DESTINATION,
)
```
