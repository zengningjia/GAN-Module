# 1、 	此模型训练时采用的数据集为NYU Depth Dataset V2数据集，
# 		wget -O data.mat http://horatio.cs.nyu.edu/mit/silberman/nyu_depth_v2/nyu_depth_v2_labeled.mat 使用此命令下载数据集
# 		运行extract.py从数据集中提取图像，提取的图像放在A,B两个文件夹中，A中是带雾图像，B中是对应的五雾图像。
# 		正式使用时在A中放carla的带雾图像，B中放对应的无雾图像。确保图的尺寸是（256,256,3）
# 		原作者采用了vgg-19模型提取感知损失,从这个链接'https://mega.nz/#!xZ8glS6J!MAnE91ND_WyfZ_8mvkuSa2YcA7q-1ehfSm-Q1fxOvvs'下载vgg模型的参数.
# 		运行main.py训练模型
#		训练模型的命令为：python main.py --A_dir=A --B_dir=B --batch_size=2 --epochs=20 --custom_data=true --mode=train --save_samples=false
#		注意custom_data要设置为true.各参数具体功能参看main函数
#		在模型训练的过程中，可以在每次保存checkpoint的时候输出当前模型跑出来的图像情况。
#		实现的方法是在项目文件夹中新建文件夹命名为samples（名字可变），里面存放符合格式的带雾图像文件
#		然后命令行修改一下以下参数：--save_samples=true --sample_image_dir=samples，然后执行。
#		在训练完模型后我们可以在文件夹model（或者你修改的model_name对应的文件夹）中的checkpoint找到训练结果，默认保存的是后三次的checkpoint。
#
# 2、	运行以下命令行测试模型 python main.py --A_dir=input_dir --B_dir=GT_dir --mode=test
#		其中input_dir为存放待处理带雾图像的文件夹，GT_dir为存放对应无雾图像的文件夹，该命令会将带雾图像放到模型中处理，
#		然后把处理后图像与ground truth图像进行对比得到Score、PSNR、SSIM显示在控制台。
#
# 3、	运行以下命令行应用模型（同样要参考main.py可以查看各参数说明）：python main.py --A_dir=input_dir --B_dir=result_dir --mode=inference
#		其中input_dir为存放待处理带雾图像的文件夹，result_dir为存放对应的处理后图像的文件夹，该命令会将带雾图像放到模型中处理，然后把处理后图像存放到result_dir中。
#
# 4、   运行环境：
#        TensorFlow (version 1.4+)
#        Matplotlib
#        Numpy
#        Scikit-Image
#       CUDA Toolkit 10.1 + cuDNN SDK 7.6 