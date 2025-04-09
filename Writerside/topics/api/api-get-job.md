#  作业查询接口

<api-doc openapi-path="../../specifications/getJob.yaml">
  <api-endpoint endpoint="/slurmdb/{version}/job/{jobId}" method="GET">
        <response type="200">
          <sample>
            {
  "jobs": [
    {
      "account": "zuhu0402",
      "comment": {
        "administrator": "",
        "job": "",
        "system": ""
      },
      "allocation_nodes": 1,
      "array": {
        "job_id": 0,
        "limits": {
          "max": {
            "running": {
              "tasks": 0
            }
          }
        },
        "task_id": {
          "set": false,
          "infinite": false,
          "number": 0
        },
        "task": ""
      },
      "association": {
        "account": "zuhu0402",
        "cluster": "slurm24",
        "partition": "",
        "user": "zuhu0402",
        "id": 14
      },
      "block": "",
      "cluster": "slurm24",
      "constraints": "",
      "container": "",
      "derived_exit_code": {
        "status": [
          "SUCCESS"
        ],
        "return_code": {
          "set": true,
          "infinite": false,
          "number": 0
        },
        "signal": {
          "id": {
            "set": false,
            "infinite": false,
            "number": 0
          },
          "name": ""
        }
      },
      "time": {
        "elapsed": 0,
        "eligible": 1744187887,
        "end": 1744187888,
        "start": 1744187888,
        "submission": 1744187887,
        "suspended": 0,
        "system": {
          "seconds": 0,
          "microseconds": 0
        },
        "limit": {
          "set": false,
          "infinite": true,
          "number": 0
        },
        "total": {
          "seconds": 0,
          "microseconds": 0
        },
        "user": {
          "seconds": 0,
          "microseconds": 0
        }
      },
      "exit_code": {
        "status": [
          "SUCCESS"
        ],
        "return_code": {
          "set": true,
          "infinite": false,
          "number": 0
        },
        "signal": {
          "id": {
            "set": false,
            "infinite": false,
            "number": 0
          },
          "name": ""
        }
      },
      "extra": "",
      "failed_node": "",
      "flags": [
        "STARTED_ON_SCHEDULE",
        "START_RECEIVED"
      ],
      "group": "zuhu0402",
      "het": {
        "job_id": 0,
        "job_offset": {
          "set": false,
          "infinite": false,
          "number": 0
        }
      },
      "job_id": 26,
      "name": "t-1",
      "licenses": "",
      "mcs": {
        "label": ""
      },
      "nodes": "zznode-140",
      "partition": "test",
      "hold": false,
      "priority": {
        "set": true,
        "infinite": false,
        "number": 2
      },
      "qos": "normal",
      "required": {
        "CPUs": 1,
        "memory_per_cpu": {
          "set": false,
          "infinite": false,
          "number": 0
        },
        "memory_per_node": {
          "set": true,
          "infinite": false,
          "number": 0
        }
      },
      "kill_request_user": "",
      "reservation": {
        "id": 0,
        "name": ""
      },
      "script": "",
      "state": {
        "current": [
          "COMPLETED"
        ],
        "reason": "None"
      },
      "steps": [
        {
          "time": {
            "elapsed": 0,
            "end": {
              "set": true,
              "infinite": false,
              "number": 1744187888
            },
            "start": {
              "set": true,
              "infinite": false,
              "number": 1744187888
            },
            "suspended": 0,
            "system": {
              "seconds": 0,
              "microseconds": 0
            },
            "total": {
              "seconds": 0,
              "microseconds": 0
            },
            "user": {
              "seconds": 0,
              "microseconds": 0
            }
          },
          "exit_code": {
            "status": [
              "SUCCESS"
            ],
            "return_code": {
              "set": true,
              "infinite": false,
              "number": 0
            },
            "signal": {
              "id": {
                "set": false,
                "infinite": false,
                "number": 0
              },
              "name": ""
            }
          },
          "nodes": {
            "count": 1,
            "range": "zznode-140",
            "list": [
              "zznode-140"
            ]
          },
          "tasks": {
            "count": 1
          },
          "pid": "",
          "CPU": {
            "requested_frequency": {
              "min": {
                "set": true,
                "infinite": false,
                "number": 0
              },
              "max": {
                "set": true,
                "infinite": false,
                "number": 0
              }
            },
            "governor": "0"
          },
          "kill_request_user": "",
          "state": [
            "COMPLETED"
          ],
          "statistics": {
            "CPU": {
              "actual_frequency": 0
            },
            "energy": {
              "consumed": {
                "set": true,
                "infinite": false,
                "number": 0
              }
            }
          },
          "step": {
            "id": "26.batch",
            "name": "batch"
          },
          "task": {
            "distribution": "Unknown"
          },
          "tres": {
            "requested": {
              "max": [
              ],
              "min": [
              ],
              "average": [
              ],
              "total": [
              ]
            },
            "consumed": {
              "max": [
              ],
              "min": [
              ],
              "average": [
              ],
              "total": [
              ]
            },
            "allocated": [
              {
                "type": "cpu",
                "name": "",
                "id": 1,
                "count": 1
              },
              {
                "type": "mem",
                "name": "",
                "id": 2,
                "count": 62000
              },
              {
                "type": "node",
                "name": "",
                "id": 4,
                "count": 1
              }
            ]
          }
        }
      ],
      "submit_line": "",
      "tres": {
        "allocated": [
          {
            "type": "cpu",
            "name": "",
            "id": 1,
            "count": 1
          },
          {
            "type": "mem",
            "name": "",
            "id": 2,
            "count": 62000
          },
          {
            "type": "energy",
            "name": "",
            "id": 3,
            "count": -2
          },
          {
            "type": "node",
            "name": "",
            "id": 4,
            "count": 1
          },
          {
            "type": "billing",
            "name": "",
            "id": 5,
            "count": 1
          }
        ],
        "requested": [
          {
            "type": "cpu",
            "name": "",
            "id": 1,
            "count": 1
          },
          {
            "type": "mem",
            "name": "",
            "id": 2,
            "count": 62000
          },
          {
            "type": "node",
            "name": "",
            "id": 4,
            "count": 1
          },
          {
            "type": "billing",
            "name": "",
            "id": 5,
            "count": 1
          }
        ]
      },
      "used_gres": "",
      "user": "zuhu0402",
      "wckey": {
        "wckey": "",
        "flags": [
        ]
      },
      "working_directory": "\/home\/zuhu0402\/zuhu0402"
    }
  ],
  "meta": {
    "plugin": {
      "type": "openapi\/slurmdbd",
      "name": "Slurm OpenAPI slurmdbd",
      "data_parser": "data_parser\/v0.0.40",
      "accounting_storage": "accounting_storage\/slurmdbd"
    },
    "client": {
      "source": "[::]:9927",
      "user": "nobody",
      "group": "nobody"
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
  ]
}
          </sample>
        </response>
  </api-endpoint>
</api-doc>

<api-doc openapi-path="../../specifications/getJobs.yaml">
<api-endpoint endpoint="/slurmdb/{version}/jobs" method="GET">
        <response type="200">
          <sample>
            {
  "jobs": [
    {
      "account": "zuhu0402",
      "comment": {
        "administrator": "",
        "job": "",
        "system": ""
      },
      "allocation_nodes": 1,
      "array": {
        "job_id": 0,
        "limits": {
          "max": {
            "running": {
              "tasks": 0
            }
          }
        },
        "task_id": {
          "set": false,
          "infinite": false,
          "number": 0
        },
        "task": ""
      },
      "association": {
        "account": "zuhu0402",
        "cluster": "slurm24",
        "partition": "",
        "user": "zuhu0402",
        "id": 14
      },
      "block": "",
      "cluster": "slurm24",
      "constraints": "",
      "container": "",
      "derived_exit_code": {
        "status": [
          "SUCCESS"
        ],
        "return_code": {
          "set": true,
          "infinite": false,
          "number": 0
        },
        "signal": {
          "id": {
            "set": false,
            "infinite": false,
            "number": 0
          },
          "name": ""
        }
      },
      "time": {
        "elapsed": 0,
        "eligible": 1744187887,
        "end": 1744187888,
        "start": 1744187888,
        "submission": 1744187887,
        "suspended": 0,
        "system": {
          "seconds": 0,
          "microseconds": 0
        },
        "limit": {
          "set": false,
          "infinite": true,
          "number": 0
        },
        "total": {
          "seconds": 0,
          "microseconds": 0
        },
        "user": {
          "seconds": 0,
          "microseconds": 0
        }
      },
      "exit_code": {
        "status": [
          "SUCCESS"
        ],
        "return_code": {
          "set": true,
          "infinite": false,
          "number": 0
        },
        "signal": {
          "id": {
            "set": false,
            "infinite": false,
            "number": 0
          },
          "name": ""
        }
      },
      "extra": "",
      "failed_node": "",
      "flags": [
        "STARTED_ON_SCHEDULE",
        "START_RECEIVED"
      ],
      "group": "zuhu0402",
      "het": {
        "job_id": 0,
        "job_offset": {
          "set": false,
          "infinite": false,
          "number": 0
        }
      },
      "job_id": 26,
      "name": "t-1",
      "licenses": "",
      "mcs": {
        "label": ""
      },
      "nodes": "zznode-140",
      "partition": "test",
      "hold": false,
      "priority": {
        "set": true,
        "infinite": false,
        "number": 2
      },
      "qos": "normal",
      "required": {
        "CPUs": 1,
        "memory_per_cpu": {
          "set": false,
          "infinite": false,
          "number": 0
        },
        "memory_per_node": {
          "set": true,
          "infinite": false,
          "number": 0
        }
      },
      "kill_request_user": "",
      "reservation": {
        "id": 0,
        "name": ""
      },
      "script": "",
      "state": {
        "current": [
          "COMPLETED"
        ],
        "reason": "None"
      },
      "steps": [
        {
          "time": {
            "elapsed": 0,
            "end": {
              "set": true,
              "infinite": false,
              "number": 1744187888
            },
            "start": {
              "set": true,
              "infinite": false,
              "number": 1744187888
            },
            "suspended": 0,
            "system": {
              "seconds": 0,
              "microseconds": 0
            },
            "total": {
              "seconds": 0,
              "microseconds": 0
            },
            "user": {
              "seconds": 0,
              "microseconds": 0
            }
          },
          "exit_code": {
            "status": [
              "SUCCESS"
            ],
            "return_code": {
              "set": true,
              "infinite": false,
              "number": 0
            },
            "signal": {
              "id": {
                "set": false,
                "infinite": false,
                "number": 0
              },
              "name": ""
            }
          },
          "nodes": {
            "count": 1,
            "range": "zznode-140",
            "list": [
              "zznode-140"
            ]
          },
          "tasks": {
            "count": 1
          },
          "pid": "",
          "CPU": {
            "requested_frequency": {
              "min": {
                "set": true,
                "infinite": false,
                "number": 0
              },
              "max": {
                "set": true,
                "infinite": false,
                "number": 0
              }
            },
            "governor": "0"
          },
          "kill_request_user": "",
          "state": [
            "COMPLETED"
          ],
          "statistics": {
            "CPU": {
              "actual_frequency": 0
            },
            "energy": {
              "consumed": {
                "set": true,
                "infinite": false,
                "number": 0
              }
            }
          },
          "step": {
            "id": "26.batch",
            "name": "batch"
          },
          "task": {
            "distribution": "Unknown"
          },
          "tres": {
            "requested": {
              "max": [
              ],
              "min": [
              ],
              "average": [
              ],
              "total": [
              ]
            },
            "consumed": {
              "max": [
              ],
              "min": [
              ],
              "average": [
              ],
              "total": [
              ]
            },
            "allocated": [
              {
                "type": "cpu",
                "name": "",
                "id": 1,
                "count": 1
              },
              {
                "type": "mem",
                "name": "",
                "id": 2,
                "count": 62000
              },
              {
                "type": "node",
                "name": "",
                "id": 4,
                "count": 1
              }
            ]
          }
        }
      ],
      "submit_line": "",
      "tres": {
        "allocated": [
          {
            "type": "cpu",
            "name": "",
            "id": 1,
            "count": 1
          },
          {
            "type": "mem",
            "name": "",
            "id": 2,
            "count": 62000
          },
          {
            "type": "energy",
            "name": "",
            "id": 3,
            "count": -2
          },
          {
            "type": "node",
            "name": "",
            "id": 4,
            "count": 1
          },
          {
            "type": "billing",
            "name": "",
            "id": 5,
            "count": 1
          }
        ],
        "requested": [
          {
            "type": "cpu",
            "name": "",
            "id": 1,
            "count": 1
          },
          {
            "type": "mem",
            "name": "",
            "id": 2,
            "count": 62000
          },
          {
            "type": "node",
            "name": "",
            "id": 4,
            "count": 1
          },
          {
            "type": "billing",
            "name": "",
            "id": 5,
            "count": 1
          }
        ]
      },
      "used_gres": "",
      "user": "zuhu0402",
      "wckey": {
        "wckey": "",
        "flags": [
        ]
      },
      "working_directory": "\/home\/zuhu0402\/zuhu0402"
    }
  ],
  "meta": {
    "plugin": {
      "type": "openapi\/slurmdbd",
      "name": "Slurm OpenAPI slurmdbd",
      "data_parser": "data_parser\/v0.0.40",
      "accounting_storage": "accounting_storage\/slurmdbd"
    },
    "client": {
      "source": "[::]:9927",
      "user": "nobody",
      "group": "nobody"
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
  ]
}
          </sample>
        </response>
  </api-endpoint>
</api-doc>