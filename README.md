# WxRedPack
微信红包(wechat redpack api) php版，基于官方的rest api做了封装和测试，避了一些坑
调用者只需要引入工程的WxRedPackHelper.php，其余的WxPayApi直接使用微信官方的支付api代码即可。

# 以下是示例

        // 发送单个红包
        $param = ["nonce_str" => \WxPayApi::getNonceStr(),//随机字符串
            "mch_billno" => $this->app_mchid . date('YmdHis') . rand(1000, 9999),//订单号
            "mch_id" => \WxPayConfig::MCHID,//商户号
            "wxappid" => \WxPayConfig::APPID,
            "send_name" => '同仁堂健康',//红包发送者名称
            "re_openid" => $openid,
            "total_amount" => 100,//付款金额，单位分
            "min_value" => 100,//最小红包金额，单位分
            "max_value" => 100,//最大红包金额，单位分
            "total_num" => 1,//红包发放总人数
            "wishing" => '恭喜发财',//红包祝福语
            "client_ip" => '127.0.0.1',//调用接口的机器 Ip 地址
            "act_name" => '红包活动',//活动名称
            "remark" => '快来抢！',//备注信息
        ];
        $wxRedPackHelper = new \WxRedPackHelper($param);
        $r = $wxRedPackHelper->send();
        
        // 发送裂变红包
        // 注意：发裂变红包不能加不必要的参数：min_value，max_value，client_ip
        $param = ["nonce_str" => \WxPayApi::getNonceStr(),//随机字符串
            "mch_billno" => $this->app_mchid . date('YmdHis') . rand(1000, 9999),//订单号
            "mch_id" => \WxPayConfig::MCHID,//商户号
            "wxappid" => \WxPayConfig::APPID,
            "send_name" => '同仁堂健康',//红包发送者名称
            "re_openid" => $openid,
            "total_amount" => 300,//付款金额，单位分
            "total_num" => 3,//红包发放总人数
            "amt_type" => 'ALL_RAND',//红包金额设置方式，ALL_RAND—全部随机
            "wishing" => '恭喜发财',//红包祝福语
            "act_name" => '红包活动',//活动名称
            "remark" => '快来抢！',//备注信息
        ];
        $wxRedPackHelper = new \WxRedPackHelper($param);
        $r = $wxRedPackHelper->send_group();
