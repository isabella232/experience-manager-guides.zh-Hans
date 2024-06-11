---
title: 上下文菜单
description: 自定义上下文菜单
role: User, Admin
exl-id: 25aa76dd-ef05-41ed-b980-14bbc1626059
source-git-commit: 4f00d6b7ad45636618bafe92e643b3e288ec2643
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 0%

---

# 自定义上下文菜单

可以自定义以下上下文菜单：

- `file_options`
控制器：
   - 映射视图： `ditamap_viewer_controller`
   - 存储库面板： `repository_panel_controller`
   - 收藏夹面板： `collection_tree_controller`
   - 文件属性引用链接： `file_references_links_controller`
   - 存储库搜索面板： `repository_search_controller`
   - 主题方案面板： `subject_scheme_tree_controller`

- `folder_options`
控制器：
   - 存储库面板： `repository_panel_controller`
   - 收藏夹面板： `collection_tree_controller`

- `collection_options`
控制器：
   - 收藏夹面板： `collection_tree_controller`

- `map_view_options`
控制器：
   - 映射视图： `ditamap_viewer_controller`

- `baseline_panel_menu`
控制器：
   - 基线面板： `baseline_panel`

- `preset_item_menu`
控制器：
   - 预设面板： `preset_panel`

您还可以通过定义新的唯一ID来创建自己的上下文菜单。

现在，每个上下文菜单都有一个 `controller id` 关联。 此控制器处理 `on-event` 各种上下文菜单选项的功能

让我们以一个示例来了解

```js title=customise_context_menu.js"
const fileOptions = {
    id: "file_options",
    contextMenuWidget: "repository_panel",
    view: {
            items: [
                {
                    component: "div",
                    target: {
                        key:"displayName",value: "Delete",                    
                        viewState: VIEW_STATE.REPLACE
                    }
                },
                {
                    component: "div",
                    target: {
                        key:"displayName",value: "Edit",                    
                        viewState: VIEW_STATE.REPLACE
                    }
                },
                {
                    "displayName": "Download",
                    "data": {
                      "eventid": "downloadFile"
                    },
                    "icon": "downloadFromCloud",
                    "class": "menu-separator",         
                    target: {
                        key:"displayName",value: "Duplicate",                    
                        viewState: VIEW_STATE.REPLACE
                    }
                },
            ]

    },

    controller: {
        downloadFile(){
            const path  = this.getValue('selectedItems')[0].path
            this.loader.loadDitaFile(path).then((file) => {
              function download_file(name, contents) {
                const mime_type = "text/plain";
        
                const blob = new Blob([contents], {type: mime_type});
        
                const dlink = document.createElement('a');
                dlink.download = name;
                dlink.href = window.URL.createObjectURL(blob);
                dlink.onclick = function() {
                    // revokeObjectURL needs a delay to work properly
                    const that = this;
                    setTimeout(function() {
                        window.URL.revokeObjectURL(that.href);
                    }, 1500);
                };
        
                dlink.click();
                dlink.remove();
            }
            download_file(path,file.xml)
            });
          }
    }
}
```

现在，让我们了解一下此代码在做什么。

1. `id` 用于标识要自定义的上下文菜单。
2. `contextMenuWidget` 用于定义 `widget id` 或 `component` 会调用上下文菜单并处理 `events`.

其余部分保持不变，因此 `view` 用于定义项目， `target` 标识要在何处替换、追加或追加选项以及 `contextMenuWidget` 控制器处理 `on-click` 事件。
