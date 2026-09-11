#### 22.4 4. Test deployment

curl -O curl -O https://raw.github.com/pytorch/serve/master/docs/images/3dogs.jpg
curl http://127.0.0.1:8080/predictions/ $ {MODEL\_NAME} $ -T 3dogs.jpg

You should obtain a response similar to:

[
    {
        "class_name": "dog",
        "bbox": [
            294.63409423828125,
            203.99111938476562,
            417.048583984375,
            281.62744140625
        ],
        "score": 0.9987992644309998
    },
    {
        "class_name": "dog",
        "bbox": [
            404.26019287109375,
            126.0080795288086,
            574.5091552734375,
            293.6662292480469
        ],
        "score": 0.9979367256164551
    },
    {
        "class_name": "dog",
        "bbox": [
            197.2144775390625,
            93.3067855834961,
            307.8505554199219,
            276.7560119628906
        ],
        "score": 0.993338406085968
    }
]

And you can use test_torchserver.py to compare result of torchserver and pytorch, and visualize them.

python tools/deployment/test_torchserver.py ${IMAGE_FILE} ${CONFIG_FILE} ${CHECKPOINT_FILE} ${MODEL_NAME}

[--inference-addr ${INFERENCE_ADDR}] [--device ${DEVICE}] [--score-thr ${SCORE_THR}]

Example:

python tools/deployment/test_torchserver.py \
demo/demo.jpg \
config/yolo/yolov3_d53_320_273e_coco.py \
checkpoint/yolov3_d53_320_273e_coco-421362b6.pth \

(continues on next page)