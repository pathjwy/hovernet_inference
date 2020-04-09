# HoVer-Net Inference Code

HoVer-Net ROI and WSI processing code for simultaneous nuclear segmentation and classification in histology images. <br />
If you require the model to be trained, refer to the [original repository](https://github.com/vqdang/hover_net).  <br />

[Link](https://www.sciencedirect.com/science/article/abs/pii/S1361841519301045?via%3Dihub) to Medical Image Analysis paper. 

## Repository Structure

- `src/` contains executable files used to run the model
- `misc/`contains util scripts
- `model/` contains scripts that define the architecture of the segmentation models
- `postproc/` contains post processing utils
- `config.py` is the configuration file. Paths need to be changed accordingly
- `infer.py` is the main inference file
- `JP2Image.m` and `read_region.m` are matlab scripts for processing `.jp2` WSIs

## Set up envrionment

```
conda create --name hovernet python=3.6
conda activate hovernet
pip install -r requirements.txt
```

## Running the code

Before running the code:
+ Download the HoVer-Net weights [here](https://drive.google.com/file/d/1k1GSsQkFkSjYY0eXi2Kx7Hlj8AGrhOOP/view?usp=sharing).[![Creative Commons License](https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png)](http://creativecommons.org/licenses/by-nc-sa/4.0/) (see below for licensing details)
+ In `config.py`, set: <br />
`self.inf_model_path`: location of `hovernet.npz` weights file <br />
`self.inf_output_dir`: directory where results are saved
+ If processing WSIs, set: <br />
`self.inf_wsi_ext` : WSI file extension <br />
`self.inf_wsi_dir` : directory where WSIs are located
+ If processing ROIs, set: <br />
`self.inf_imgs_ext` : ROI file extension <br />
`self.inf_data_dir` : directory where ROIs are located

Note, other hyperparameters such as batch size and WSI processing level can be tuned. Refer to comments in `config.py.` <br />

To run, use: <br />

`python infer.py --gpu=<gpu_list> --mode=<inf_mode>` <br />

`<gpu_list>` is a comma separated list indicating the GPUs to use. <br />
`<inf_mode>` is a string indicating the inference mode. Use either:

- `'roi'`
- `'wsi'`

## Citation 

If any part of this code is used, please give appropriate citation. <br />

BibTex entry: <br />
```
@article{graham2019hover,
  title={Hover-net: Simultaneous segmentation and classification of nuclei in multi-tissue histology images},
  author={Graham, Simon and Vu, Quoc Dang and Raza, Shan E Ahmed and Azam, Ayesha and Tsang, Yee Wah and Kwak, Jin Tae and Rajpoot, Nasir},
  journal={Medical Image Analysis},
  pages={101563},
  year={2019},
  publisher={Elsevier}
}

@inproceedings{gamper2019pannuke,
  title={PanNuke: an open pan-cancer histology dataset for nuclei instance segmentation and classification},
  author={Gamper, Jevgenij and Koohbanani, Navid Alemi and Benet, Ksenija and Khuram, Ali and Rajpoot, Nasir},
  booktitle={European Congress on Digital Pathology},
  pages={11--19},
  year={2019},
  organization={Springer}
}

@article{gamper2020pannuke,
  title={PanNuke Dataset Extension, Insights and Baselines},
  author={Gamper, Jevgenij and Koohbanani, Navid Alemi and Graham, Simon and Jahanifar, Mostafa and Benet, Ksenija and Khurram, Syed Ali and Azam, Ayesha and Hewitt, Katherine and Rajpoot, Nasir},
  journal={arXiv preprint arXiv:2003.10778},
  year={2020}
}
```

## Dataset

The network was trained on the PanNuke dataset, where images are of size 256x256. This explains the slight difference in the input size of HoVer-Net compared to the original paper. In this repository, we also use 3x3 valid convolution in the decoder, as opposed to 5x5 convolution in the paper to speed up inference for WSI processing. <br />

Download the PanNuke dataset [here](https://warwick.ac.uk/fac/sci/dcs/research/tia/data/pannuke).

![](dataset.png)

## License

Note that the PanNuke dataset is licensed under [Attribution-NonCommercial-ShareAlike 4.0 International](http://creativecommons.org/licenses/by-nc-sa/4.0/), therefore the derived weights for HoVer-Net are also shared under the same license. Please consider the implications of using the weights under this license on your work and it's licensing. 
