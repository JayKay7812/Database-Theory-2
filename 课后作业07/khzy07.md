# 分词服务化
## 代码
```
from flask import Flask, render_template, request, jsonify, make_response
import jieba

jieba.load_userdict("zh_dict.txt")
def cut(content):
    f1 = open("zh_tokenize_test.txt", "r",encoding='UTF-8')
    for line in f1.readlines():
        line=line.strip()
        word_list=jieba.cut(line,cut_all=False)
        print("/".join(word_list),"\n")
    f1.close()

def gen_http_result():
    res = {
        'status': 'ok',
        'msg': '',
        'data': []
    }
    return res

def make_resp(ret):
    resp = make_response(json.dumps(ret))
    resp.mimetype = 'application/json'
    resp.headers['Access-Control-Allow-Origin'] = '*'
    return resp

app = Flask(__name__)

@app.route('/hello', methods=['GET'])
def hello():
    ret = gen_http_result()
    ret['data']= "hello world"
    rsp = make_resp(ret)
    return rsp

@app.route('/tokenize', methods=['POST'])
def hello():
    ret = gen_http_result()
    postform = request.form
    sent = postform.get('sent')
    # lang = postform.get('lang')
    word_list = jieba.cut(sent)

    ret['data']= word_list
    rsp = make_resp(ret)
    return rsp

_host, _port = '0.0.0.0', 1688
app.run(host=_host,port=_port,debug=True)
```
