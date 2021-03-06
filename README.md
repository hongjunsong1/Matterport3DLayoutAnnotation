# The MatterportLayout dataset

This dataset extends the Matterport3D dataset with general Manhattan layout annotations and is used in our work "[3D Manhattan Room Layout Reconstruction from a Single 360 Image](http://arxiv.org/abs/1910.04099) for performance evaluation".

## Pre-processing
Note that we release only the annotated layout files, you have to generate corresponding RGB panoramas using the instructions as follows:
1. Download the **[Matterport3D](https://github.com/niessner/Matterport)** dataset.
2. Follow the Matlab codes in **[PanoBasic/demo_matterport.m](https://github.com/yindaz/PanoBasic/blob/master/demo_matterport.m#L44)** to stitch the skybox images of the Matterport3D into the equirectangular panoramas.
3. Run the script provided in **[PanoAnnotator/pre-process](https://github.com/SunDaDenny/PanoAnnotator#pre-process)** to generate Manhattan-aligned panoramas.

## Data format
* We are dealing with some issues with the dataset, and we will release it later. If there's an urgent need, you can send an email to me.
* **Panorama list**: The dataset includes 2295 panoramas selected from the Matterport3D dataset and we split the images into [train](data_list/mp3d_train.txt)/[val](data_list/mp3d_val.txt)/[test](data_list/mp3d_test.txt) lists.
* **Annotation format**: We use the same the annotation format as [DuLa-Net](https://github.com/SunDaDenny/DuLa-Net) and [PanoAnnotator](https://github.com/SunDaDenny/PanoAnnotator). An example json file is shown below. Please refer to these two repos for more details. Note that we've aligned all the annotated layouts to the camera height of 1.6m.
```javascript
{
    "cameraHeight": 1.6, // distance between camera and floor
    "layoutHeight": 2.9809624004364013, // distance between floor and ceiling
    "layoutObj2ds": { // door or window labeling block
        "num": 0,
        "obj2ds": []
    },
    "layoutPoints": { // corner labeling block, we only annotate the corner in the horizontal direction because you can easily get the corner in the vertical direction from cameraHeight and layoutHeight.
        "num": 6, // corner number in the horizontal direction
        "points": [ // List of the corner
            {
                "coords": [ // uv coordintate of the corner on the panorama
                    0.7081447345651483, // u coordintate of the corner on the panorama
                    0.5 // v coordintate of the corner on the panorama. We annotate on horizon line, then calculate the vertical position by cameraHeight and layoutHeight.
                ],
                "id": 0, // id number
                "xyz": [ // project the corner on to the 3D coordinate 
                    3.0078125, // x value
                    0.0, // y value
                    -0.8097623087756155 // z value
                ]
            },
            {...}
        ]
    },
    "layoutWalls": { // layout walls represented by plane equation
        "num": 6, // wall number
        "walls": [ // list of wall
            {
                "id": 0, // id number
                "normal": [ // plane equation's normal
                    1.0,
                    0.0,
                    -0.0
                ],
                "planeEquation": [ // plane equation
                    1.0, // a
                    0.0, // b
                    -0.0, // c
                    -3.0078125 // d
                ],
                "pointsIdx": [ // which two points construct this wall
                    0,
                    1
                ],
                "width": 2.8476272687756152 // the wall width
            },
            {...}
        ]
    },
    "panoId": "nothing" // a simple ID of panorama
}
```
* **File name**: The filename `<dir1>_<dir2>_label.json` follows the folder structure of Matterport3D dataset.

## Citation
If you use this dataset for your research, please cite our paper.
```
@article{zou20193d,
  title={3D Manhattan Room Layout Reconstruction from a Single 360 Image},
  author={Zou, Chuhang and Su, Jheng-Wei and Peng, Chi-Han and Colburn, Alex and Shan, Qi and Wonka, Peter and Chu, Hung-Kuo and Hoiem, Derek},
  journal={arXiv preprint arXiv:1910.04099},
  year={2019}
}
```

## License

The data is released under the [Matterport3D Terms of Use](http://kaldir.vc.in.tum.de/matterport/MP_TOS.pdf), and the code is released under the MIT license. By using this dataset, you agree to all the terms in the [Matterport3D Terms of Use](http://kaldir.vc.in.tum.de/matterport/MP_TOS.pdf).
