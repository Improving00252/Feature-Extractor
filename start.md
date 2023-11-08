# start from here

Before the start , make sure the environment is armed and ready !

To install detectron2 on linux system , you can check [detectron2_installation_on_linux.md](detectron2_installation_on_linux.md).

After the installation , switch to the backbone file , i wrote the extract code in the backbone part to observe features in different stages , so you need to replace the backbone file with [this one](FPN_backbone)
  
    cd detectron2/detectron2/modeling/backbone/FPN 
and replace with my code

then prepare clean files in demo file

    cd detectron2/demo 
    mkdir res
    cd res
    mkdir res2
    mkdir res3
    mkdir res4
    mkdir res5
    cd ..
    mkdir lateral
    cd lateral
    mkdir lateral2
    mkdir lateral3
    mkdir lateral4
    mkdir lateral5
    cd ..
    mkdir pyramid
    cd pyramid
    mkdir p2
    mkdir p3
    mkdir p4
    mkdir p5
    cd ..
now we run the demo code , and extract the feature tensors into those clean file
check those files and find whether the amount are correct , following is the tensors amount of each layers
(numbers on the right means there should be same amounts of tensor files in each layer files)

  |  layer name  |  tensor amount  |
  | :---- | :---- |
  |  res2  |  256  |
  |  res3  |  512  |
  |  res4  |  1024  |
  |  res5  |  2048  |
  |  lateral2  |  256  |
  |  lateral3  |  256  |
  |  lateral4  |  256  |
  |  lateral5  |  256  |
  |  p2  |  256  |
  |  p3  |  256  |
  |  p4  |  256  |
  |  p5  |  256  |

Those tensors are .txt file , we first find the maximum value and minimum value , then use these two values to do inverse-quantization , through this step , tensors in deffidient layers could be judged by the same standard.


Put three different python files into pyramid 、lateral 、res , change the GLOBAL_MAX and GLOBAL_MIN into the values we have .
  | for pyramid | for lateral | for res |
  | :---------- | :------------ | :------------ |
  | [pyramid](fmap_p) | [lateral](fmap_lateral) | [res](fmap_res) |

Run those files , and we dump out of those tensors.

    cd res
    python fmap_res.py
    cd lateral
    python fmap_laeral.py
    cd pyramid
    python fmap_p.py

example 原圖

  <img decoding="async" src = https://i.imgur.com/PWfNyST.jpg  width=20%> 

res

  res2<img decoding="async" src = https://i.imgur.com/qI023Wj.png >
  res3<img decoding="async" src = https://i.imgur.com/Pwv5ygs.png >
  res4<img decoding="async" src = https://i.imgur.com/gbh27eu.png >
  res5<img decoding="async" src = https://i.imgur.com/p5cubkp.png >

lateral

  lateral2<img decoding="async" src = https://i.imgur.com/Xj8GTgF.png >
  lateral3<img decoding="async" src = https://i.imgur.com/JAk9oK7.png >
  lateral4<img decoding="async" src = https://i.imgur.com/2JK5y2t.png >
  lateral5<img decoding="async" src = https://i.imgur.com/xmgh8EP.png >

pyramid
  
  pyramid2<img decoding="async" src = https://i.imgur.com/FEdLmG1.png >
  pyramid3<img decoding="async" src = https://i.imgur.com/e4Kr4Bj.png >
  pyramid4<img decoding="async" src = https://i.imgur.com/T9ZWp17.png >
  pyramid5<img decoding="async" src = https://i.imgur.com/qlucbyJ.png >
  

[(back to top)](#start-from-here)
    
    
