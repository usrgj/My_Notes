---
tags: [Ubuntu]
title: Vscode
created: '2025-08-02T11:19:10.329Z'
modified: '2025-08-03T12:56:43.179Z'
---

Vscode

#### 自定义代码模板
点击右下角齿轮
点击`snippets`
点击对应语言的json
下面是一个c++示例
```json
{
	//注意body中的代码每一行要用 "" 引起，同时使用逗号分割开
	//在代码中是使用的Tab键缩进，模板中需要使用空格键，将缩进全改为空格即可
	//这是因为""中有引号嵌套，在里面的引号中加上\即可
	"Print to console": {
		"prefix": "ros2_main_cpp",//trigger keywords
		"body": [ // template body
			"//包含头文件",
			"#include <rclcpp/rclcpp.hpp>",
			"// 自定义节点类",
			"class My_node :public rclcpp::Node{",
			"public:",
			"    My_node():Node(\"My_node_node\"){",
			"        RCLCPP_INFO(this->get_logger(),\"启动成功\");",
			"    }",
			"",
           "};",
			"",
			"int main(int argc,char **argv){",
			"  // 初始化ROS2客户端",
			"  rclcpp::init(argc,argv);",
			"  //调用spin函数，传入指针",
			"  rclcpp::spin(std::make_shared<My_node>());",
			"  //释放资源",
			"  rclcpp::shutdown();",
			"  return 0;",
			"}",
		],
		"description": "ros2 main func" // description of the template
	},

	"ttt":{
		"prefix": "test",
		"body": [
			"testhhhhhh",
		],
	}
}

```

#### 快捷键
|场景|shortcut|作用|
|---|---|---|
|编辑器|`ctrl + shift + i`|全局代码自动缩进，整理格式|
||``||
