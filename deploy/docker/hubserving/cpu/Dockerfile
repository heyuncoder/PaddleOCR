# Version: 1.0.0
FROM hub.baidubce.com/paddlepaddle/paddle:1.8.5-gpu-cuda9.0-cudnn7

# PaddleOCR base on Python3.7
RUN pip3.7 install --upgrade pip -i https://pypi.tuna.tsinghua.edu.cn/simple

RUN python3.7 -m pip install paddlepaddle==1.8.5 -i https://pypi.tuna.tsinghua.edu.cn/simple

RUN pip3.7 install paddlehub --upgrade -i https://pypi.tuna.tsinghua.edu.cn/simple

RUN cd / && git clone git@github.com:heyuncoder/PaddleOCR.git

WORKDIR /PaddleOCR

RUN pip3.7 install -r requirments.txt -i https://pypi.tuna.tsinghua.edu.cn/simple

RUN mkdir -p /PaddleOCR/inference
# Download orc detect model(light version). if you want to change normal version, you can change ch_det_mv3_db_infer to ch_det_r50_vd_db_infer, also remember change det_model_dir in deploy/hubserving/ocr_system/params.py）
# ADD https://paddleocr.bj.bcebos.com/ch_models/ch_det_mv3_db_infer.tar /PaddleOCR/inference
ADD https://paddleocr.bj.bcebos.com/20-09-22/server/det/ch_ppocr_server_v1.1_det_infer.tar /PaddleOCR/inference
# RUN tar xf /PaddleOCR/inference/ch_det_mv3_db_infer.tar -C /PaddleOCR/inference
RUN tar xf /PaddleOCR/inference/ch_ppocr_server_v1.1_det_infer.tar -C /PaddleOCR/inference

# Download orc recognition model(light version). If you want to change normal version, you can change ch_rec_mv3_crnn_infer to ch_rec_r34_vd_crnn_enhance_infer, also remember change rec_model_dir in deploy/hubserving/ocr_system/params.py）
# ADD https://paddleocr.bj.bcebos.com/ch_models/ch_rec_mv3_crnn_infer.tar /PaddleOCR/inference
ADD https://paddleocr.bj.bcebos.com/20-09-22/server/rec/ch_ppocr_server_v1.1_rec_infer.tar /PaddleOCR/inference
# RUN tar xf /PaddleOCR/inference/ch_rec_mv3_crnn_infer.tar -C /PaddleOCR/inference
RUN tar xf /PaddleOCR/inference/ch_ppocr_server_v1.1_rec_infer.tar -C /PaddleOCR/inference

# ADD https://paddleocr.bj.bcebos.com/20-09-22/cls/ch_ppocr_mobile_v1.1_cls_infer.tar /PaddleOCR/inference
# RUN tar xf /PaddleOCR/inference/ch_ppocr_mobile_v1.1_cls_infer.tar -C /PaddleOCR/inference


EXPOSE 8866

CMD ["/bin/bash","-c","export PYTHONPATH=. && hub install deploy/hubserving/ocr_system/ && hub serving start -m ocr_system"]