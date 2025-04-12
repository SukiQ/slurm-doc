#  作业提交接口

<api-doc openapi-path="../../specifications/submitJob.yaml">
  <api-endpoint endpoint="/slurm/{version}/job/submit" method="POST">
 <request>
        <sample lang="JSON" title="Example">
          {
    "job": {
        "name": "t-1", 
        "nodes": "1", 
        "partition": "test", 
        "script": "#!/bin/bash\necho \"开始调用仿真软件“\nsleep 600\necho \"仿真软件执行完成", 
        "exclusive": false, 
        "priority": {
            "set": true, 
            "infinite": false, 
            "number": 2
        }, 
        "environment": [
            "/usr/local/munge/lib:/usr/local/slurm/lib64"
        ], 
        "cpus_per_task": 1, 
        "current_working_directory": "/home/zuhu0402/zuhu0402", 
        "standard_output": "/home/zuhu0402/zuhu0402/stdout_1744187887142", 
        "standard_error": "/home/zuhu0402/zuhu0402/stderr_1744187887142", 
        "standard_input": "/dev/null", 
        "required_nodes": [
            "sivi-140"
        ], 
        "group_id": 10144, 
        "user_id": 10154
    }
}
        </sample>
    </request>
        <response type="200">
          <sample>
             {
  "result": {
    "job_id": 26,
    "step_id": "batch",
    "error_code": 0,
    "error": "No error",
    "job_submit_user_msg": ""
  },
  "job_id": 26,
  "step_id": "batch",
  "job_submit_user_msg": "",
  "meta": {
    "plugin": {
      "type": "openapi\/slurmctld",
      "name": "Slurm OpenAPI slurmctld",
      "data_parser": "data_parser\/v0.0.40",
      "accounting_storage": "accounting_storage\/slurmdbd"
    },
    "client": {
      "source": "[::]:5319",
      "user": "root",
      "group": "root"
    },
    "command": [
    ],
    "slurm": {
      "version": {
        "major": "24",
        "micro": "4",
        "minor": "05"
      },
      "release": "24.05.4",
      "cluster": "slurm24"
    }
  },
  "errors": [
  ],
  "warnings": [
    {
      "description": "Expected OpenAPI type=string (Slurm type=string) but got OpenAPI type=integer (Slurm type=64 bit integer)",
      "source": "#\/job\/group_id\/"
    },
    {
      "description": "Expected OpenAPI type=string (Slurm type=string) but got OpenAPI type=integer (Slurm type=64 bit integer)",
      "source": "#\/job\/user_id\/"
    }
  ]
}
          </sample>
        </response>
  </api-endpoint>
</api-doc>