---
title: Documentation
layout: posts
permalink: /documentation/

collection: posts

classes: wide

sidebar:
  nav: "docs"
---

## Project

### Definition

    Version: 1.0.
    Package: Project Information.
    Design: Graph and circuit design.
    Dependencies: All used dependencies in one level.

Extension: .vc


### Block Instances

```
{
  "version": "1.0",
  "package": {
    "name": "",
    "version": "",
    "description": "",
    "author": "",
    "image": ""
  },
  "design": {
    "board": "",
    "graph": {
      "blocks": [],
      "wires": []
    }
  },
  "dependencies": {}
}
```


### Wire Instances


```
{
  "source": {
    "block": "",
    "port": ""
  },
  "target": {
    "block": "",
    "port": ""
  },
  "vertices": [
    {
      "x": 0,
      "y": 0
    }
  ]
}
```

### Project Information

    Name
    Version
    Description
    Author
    Image (SVG)
    
# Insert Image Here.


## Samples

### Camera

<details><summary>Camera.vc</summary>
<p>

```
{
  "version": "1.0",
  "package": {
    "name": "Camera",
    "version": "1.0.0",
    "description": "Captures Video Stream from Camera",
    "author": "Muhammad Taha Suhail",
    "image": ""
  },
  "design": {
    "board": "Python3-Noetic",
    "graph": {
      "blocks": [

        {
          "id": "200",
          "type": "basic.output",
          "data": {
            "name": "",
            "pins": [
              {
                "index": "0",
                "name": "",
                "value": "0"
              }
            ],
            "virtual": true
          },
          "position": {
            "x": 752,
            "y": 144
          }
        },
        
        {
          "id": "300",
          "type": "basic.code",
          "data": {
            "code": "import cv2\r\nimport numpy as np\r\nfrom time import sleep\r\nfrom wires.wire_img import Wire_Write\r\n\r\ndef Camera(input_wires, output_wires, parameters):\r\n\r\n    cap = cv2.VideoCapture(0)\r\n\r\n    shm_w = Wire_Write(output_wires[0])\r\n\r\n    try:\r\n        while True:\r\n            ret, frame = cap.read()\r\n            shm_w.add(frame)\r\n    except KeyboardInterrupt:\r\n        pass\r\n\r\n    shm_w.release()",
            "params": [],
            "ports": {
              "out": [
                {
                  "name": "200"
                }
              ]
            }
          },
          "position": {
            "x": 248,
            "y": 88
          },
          "size": {
            "width": 384,
            "height": 256
          }
        }
        
      ],
      "wires": [
        {
          "source": {
            "block": "",
            "port": ""
          },
          "target": {
            "block": "200",
            "port": "out"
          }
        }
      ]
    }
  },
  "dependencies": {}
}
```

</p>
</details>




### Screen

<details><summary>Screen.vc</summary>
<p>

```
{
  "version": "1.0",
  "package": {
    "name": "Screen",
    "version": "1.0.0",
    "description": "Displays Image or Video",
    "author": "Muhammad Taha Suhail",
    "image": ""
  },
  "design": {
    "board": "Python3-Noetic",
    "graph": {
      "blocks": 
   [

        {
          "id": "100",
          "type": "basic.input",
          "data": {
            "name": "",
            "pins": [
              {
                "index": "0",
                "name": "",
                "value": "0"
              }
            ],
            "virtual": true
          },
          "position": {
            "x": 64,
            "y": 144
          }
        },
        
       {
          "id": "300",
          "type": "basic.code",
          "data": {
            "code": "import cv2\nimport numpy as np\nfrom time import sleep\nfrom wires.wire_img import Wire_Read\n\ndef Screen(input_wires, output_wires, parameters):\n\n    shm_r = Wire_Read(input_wires[0])\n\n    while True:\n        sleep(0.03)\n        f = shm_r.get()\n        cv2.imshow('Screen', f)\n        if cv2.waitKey(1) & 0xFF == ord('q'):\n             break\n\n    shm_r.release()",
            "params": [],
            "ports": {
              "in": [
                {
                  "name": "100"
                }
              ]
            }
          },
          "position": {
            "x": 248,
            "y": 88
          },
          "size": {
            "width": 384,
            "height": 256
          }
        }

   ],

      "wires": 
    [

        {
          "source": {
            "block": "100",
            "port": "in"
          },
          "target": {
            "block": "",
            "port": ""
          }
        }

      ]
    }
  },
  "dependencies": {}
}
```
</p>
</details>



### Edge Detector

<details><summary>EdgeDetector.vc</summary>
<p>
  
```
{
  "version": "1.0",
  "package": {
    "name": "EdgeDetector",
    "version": "1.0.0",
    "description": "Performs Edge Detection on Image",
    "author": "Muhammad Taha Suhail",
    "image": ""
  },
  "design": {
    "board": "Python3-Noetic",
    "graph": {
      "blocks": [

        {
          "id": "100",
          "type": "basic.input",
          "data": {
            "name": "",
            "pins": [
              {
                "index": "0",
                "name": "",
                "value": "0"
              }
            ],
            "virtual": true
          },
          "position": {
            "x": 64,
            "y": 144
          }
        },

        {
          "id": "200",
          "type": "basic.output",
          "data": {
            "name": "",
            "pins": [
              {
                "index": "0",
                "name": "",
                "value": "0"
              }
            ],
            "virtual": true
          },
          "position": {
            "x": 752,
            "y": 144
          }
        },

       {
          "id": "300",
          "type": "basic.code",
          "data": {
            "code": "import cv2 as cv\nimport numpy as np\nfrom time import sleep\nfrom wires.wire_img import Wire_Read, Wire_Write\n\ndef EdgeDetector(input_wires, output_wires, parameters):\n\n    shm_r = Wire_Read(input_wires[0])\n    shm_w = Wire_Write(output_wires[0])\n    #aperture = float(parameters[0])\n\n    while True:\n\n        sleep(0.03)\n\n        frame = shm_r.get()\n        frame = cv.cvtColor(frame, cv.COLOR_BGR2GRAY)\n        edge_img = cv.Canny(frame, 100, 200)\n        edge_img = cv.cvtColor(edge_img, cv.COLOR_GRAY2BGR)\n\n        shm_w.add(edge_img)\n\n    shm_r.release()\n    shm_w.release()",
            "params": [],
            "ports": {
              "in": [
                {
                  "name": "100"
                }
              ],
              "out": [
                {
                  "name": "200"
                }
              ]
            }
          },
          "position": {
            "x": 248,
            "y": 88
          },
          "size": {
            "width": 384,
            "height": 256
          }
        },
        
        {
          "id": "400",
          "type": "basic.constant",
          "data": {
            "name": "Lower Thresh",
            "value": "100",
            "local": true
          },
          "position": {
            "x": 192,
            "y": 112
          }
        },
        {
          "id": "401",
          "type": "basic.constant",
          "data": {
            "name": "Upper Thresh",
            "value": "200",
            "local": true
          },
          "position": {
            "x": 328,
            "y": 112
          }
        }
        
      ],

      "wires": [
        {
          "source": {
            "block": "",
            "port": ""
          },
          "target": {
            "block": "",
            "port": ""
          }
        },

        {
          "source": {
            "block": "",
            "port": ""
          },
          "target": {
            "block": "",
            "port": ""
          }
        }
      ]
    }
  },
  "dependencies": {}
}
```

</p>
</details>

## Templates

For more information about how to create your own blocks from scratch, head over to this [link](https://github.com/JdeRobot/VisualCircuit/tree/master/samples)


# Block Library


### Camera

- Description: Captures Video Stream from Camera
- Input: None
- Output: BGR Image
- Parameters: None

### Color Filter

- Description: Filters a Color in an Image
- Input: BGR Image
- Output: BGR Image Filtered
- Parameters: Lower Color Range, Upper Color Range

### Contour Detector

- Description: Draws Contours in an Image
- Input: BGR Image
- Output: Contour Info(x,y,width,height,angle of rotation), BGR Image.
- Parameters: None

### Blur

- Description: Blurs an Image
- Input: BGR Image
- Output: BGR Image Blurred
- Parameters: Type (Averaging, Median, Gaussian), Kernel

### Cropper

- Description: Crops an Image.
- Input: BGR Image.
- Output: BGR Image Resized.
- Parameters: x,y,width,height

### Edge Detector

- Description: Performs Edge Detection on an Image.
- Input: BGR Image
- Output: BGR Image
- Parameters: Lower Thresh, Upper Thresh

### Face Detector

- Description: Detects Faces in an Image.
- Input: BGR Image
- Output: BGR Image with Detections.
- Parameters: Bounding Box Info ('box') / Image with Detections ('image')

### Image Read

- Description: Reads an image from a Path.
- Input: None
- Output: BGR Image
- Parameters: Image Path

### Screen

- Description: Displays an Image.
- Input: BGR Image
- Output: None
- Parameters: None

### Threshold

- Description: Thresholds an Image.
- Input: BGR Image
- Output: BGR Image Threshed
- Parameters: Thresh Value

