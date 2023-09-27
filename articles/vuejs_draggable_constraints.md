<!--
title:   【vue.js】ドラッグアンドドロップの制約と制限：制御されたドラッグ操作の実装手法
tags:    JavaScript,Vue.js
id:      ad90d4ae80ba897f12e6
private: false
-->


## ドラッグ操作の制約と許可条件の設定方法

ドラッグアンドドロップは、ユーザーが要素をドラッグして別の位置に移動する操作であり、ユーザビリティの向上や操作性の改善に役立つ機能です。vue.jsでも簡単にドラッグアンドドロップの実装が可能ですが、特定の制約や許可条件を設定することもできます。本章では、ドラッグ操作の制約と許可条件の設定方法について解説します。

### 制約条件の設定
ドラッグ操作の制約条件として、例えばドラッグを許可する要素の種類を制限したり、特定の領域内のみでのドラッグを許可したりすることができます。vue.jsでは、ドラッグ操作を制御するためのディレクティブを使用します。

```javascript
<template>
  <div id="app">
    <div v-draggable="{ allowdrag: true }">ドラッグ操作が許可されています</div>
    <div v-draggable="{ allowdrag: false }">ドラッグ操作が許可されていません</div>
  </div>
</template>

<script>
export default {
  directives: {
    draggable: {
      inserted(el, binding) {
        const allowdrag = binding.value.allowdrag;
        if (!allowdrag) {
          el.classlist.add("no-drag");
        }
      }
    }
  }
};
</script>

<style scoped>
.no-drag {
  pointer-events: none;
  opacity: 0.5;
}
</style>
```

上記のコードでは、`v-draggable`ディレクティブを使用して要素のドラッグ操作を制御しています。`allowdrag`というプロパティを指定することで、ドラッグ操作を許可(`true`)または不許可(`false`)にすることができます。cssクラス`.no-drag`を追加することで、ドラッグ操作が不許可の場合に要素を半透明にする効果を実現しています。

### 許可条件の設定
ドラッグ操作の許可条件を設定することにより、特定の要素や領域でのみドラッグ操作が可能となります。vue.jsでは、要素や領域に対して許可条件を設定することができます。

```javascript
<template>
  <div id="app">
    <div v-draggable="{ allowdrag: true, handle: '.handle' }">
      <div class="handle">ハンドル</div>
      <div>ドラッグ可能な要素</div>
    </div>
    <div v-draggable="{ allowdrag: true, containment: '.container' }">
      <div class="container">
        <div>ドラッグ可能な要素</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  directives: {
    draggable: {
      inserted(el, binding) {
        const allowdrag = binding.value.allowdrag;
        const handle = binding.value.handle;
        const containment = binding.value.containment;

        if (allowdrag) {
          if (handle) {
            const handleelement = el.queryselector(handle);
            handleelement.classlist.add("handle");
          }

          if (containment) {
            const containmentelement = el.queryselector(containment);
            el.style.left = "0";
            el.style.top = "0";
            el.style.width = `${containmentelement.offsetwidth}px`;
            el.style.height = `${containmentelement.offsetheight}px`;
          }
        }
      }
    }
  }
};
</script>

<style scoped>
.handle {
  cursor: move;
}

.container {
  width: 200px;
  height: 200px;
  border: 1px solid #ccc;
}
</style>
```

上記のコードでは、`handle`プロパティと`containment`プロパティを使用して許可条件を設定しています。`handle`プロパティでは、ドラッグ操作が有効な要素を指定することができます。指定した要素がドラッグされると、その要素だけが移動可能となります。

`containment`プロパティでは、ドラッグ可能な領域を指定することができます。指定した要素内でのみドラッグが有効となり、領域外に要素が移動することはありません。

## ドラッグ可能な要素の制限範囲と境界値の設定手法

ドラッグ操作において、要素の移動可能範囲を制限することがあります。vue.jsでは、ドラッグ可能な要素の制限範囲と境界値の設定を行うことができます。

### 制限範囲の設定
要素の移動可能範囲を制限するには、cssの`left`と`top`プロパティを適切に設定します。

```javascript
<template>
  <div id="app">
    <div v-draggable="{ allowdrag: true, minleft: -100, maxleft: 100, mintop: -100, maxtop: 100 }">
      ドラッグ可能な要素
    </div>
  </div>
</template>

<script>
export default {
  directives: {
    draggable: {
      inserted(el, binding) {
        const allowdrag = binding.value.allowdrag;
        const minleft = binding.value.minleft;
        const maxleft = binding.value.maxleft;
        const mintop = binding.value.mintop;
        const maxtop = binding.value.maxtop;

        if (allowdrag) {
          el.addeventlistener("mousedown", handlemousedown);

          function handlemousedown(e) {
            e.preventdefault();
            const startx = e.clientx;
            const starty = e.clienty;
            const startleft = parseint(getcomputedstyle(el).left, 10) || 0;
            const starttop = parseint(getcomputedstyle(el).top, 10) || 0;

            document.addeventlistener("mousemove", handlemousemove);
            document.addeventlistener("mouseup", handlemouseup);

            function handlemousemove(e) {
              const diffx = e.clientx - startx;
              const diffy = e.clienty - starty;

              let newleft = startleft + diffx;
              let newtop = starttop + diffy;

              if (minleft !== undefined && newleft < minleft) {
                newleft = minleft;
              }

              if (maxleft !== undefined && newleft > maxleft) {
                newleft = maxleft;
              }

              if (mintop !== undefined && newtop < mintop) {
                newtop = mintop;
              }

              if (maxtop !== undefined && newtop > maxtop) {
                newtop = maxtop;
              }

              el.style.left = `${newleft}px`;
              el.style.top = `${newtop}px`;
            }

            function handlemouseup(e) {
              document.removeeventlistener("mousemove", handlemousemove);
              document.removeeventlistener("mouseup", handlemouseup);
            }
          }
        }
      }
    }
  }
};
</script>

<style scoped>
#app {
  position: relative;
  width: 300px;
  height: 300px;
  border: 1px solid #ccc;
}

div {
  position: absolute;
  background-color: #f2f2f2;
  padding: 10px;
  border: 1px solid #ccc;
  cursor: move;
}
</style>
```

上記のコードでは、`minleft`、`maxleft`、`mintop`、`maxtop`というプロパティを使用して、要素の移動可能範囲を制限しています。これにより、要素が画面外に移動しないようにすることができます。

### 境界値の設定
要素の移動可能範囲を制限する際に、特定の位置を境界値として設定することもあります。境界値を設定するには、`left`、`top`プロパティの値を制御することで実現できます。

```javascript
<template>
  <div id="app">
    <div v-draggable="{ allowdrag: true, boundaryx: 50, boundaryy: 50 }">
      ドラッグ可能な要素
    </div>
  </div>
</template>

<script>
export default {
  directives: {
    draggable: {
      inserted(el, binding) {
        const allowdrag = binding.value.allowdrag;
        const boundaryx = binding.value.boundaryx;
        const boundaryy = binding.value.boundaryy;

        if (allowdrag) {
          el.addeventlistener("mousedown", handlemousedown);

          function handlemousedown(e) {
            e.preventdefault();
            const startx = e.clientx;
            const starty = e.clienty;
            const startleft = parseint(getcomputedstyle(el).left, 10) || 0;
            const starttop = parseint(getcomputedstyle(el).top, 10) || 0;

            document.addeventlistener("mousemove", handlemousemove);
            document.addeventlistener("mouseup", handlemouseup);

            function handlemousemove(e) {
              const diffx = e.clientx - startx;
              const diffy = e.clienty - starty;

              let newleft = startleft + diffx;
              let newtop = starttop + diffy;

              if (boundaryx !== undefined) {
                if (newleft <= boundaryx) {
                  newleft = boundaryx;
                } else if (newleft >= window.innerwidth - boundaryx - el.offsetwidth) {
                  newleft = window.innerwidth - boundaryx - el.offsetwidth;
                }
              }

              if (boundaryy !== undefined) {
                if (newtop <= boundaryy) {
                  newtop = boundaryy;
                } else if (newtop >= window.innerheight - boundaryy - el.offsetheight) {
                  newtop = window.innerheight - boundaryy - el.offsetheight;
                }
              }

              el.style.left = `${newleft}px`;
              el.style.top = `${newtop}px`;
            }

            function handlemouseup(e) {
              document.removeeventlistener("mousemove", handlemousemove);
              document.removeeventlistener("mouseup", handlemouseup);
            }
          }
        }
      }
    }
  }
};
</script>

<style scoped>
#app {
  position: relative;
  width: 100%;
  height: 100vh;
  background-color: #f2f2f2;
}

div {
  position: absolute;
  background-color: #ccc;
  padding: 10px;
  border: 1px solid #333;
  cursor: move;
}
</style>
```

上記のコードでは、`boundaryx`と`boundaryy`というプロパティを使用して要素の移動可能範囲に境界値を設定しています。これにより、要素が指定した境界値よりも外側に移動しないようにすることができます。

## ドロップゾーンの制限と受け入れ条件の実装方法

ドラッグアンドドロップでは、要素をドロップするゾーンを制限したり、どの要素をドロップできるかを制限したりすることができます。vue.jsでは、ドロップゾーンの制限と受け入れ条件の実装が可能です。

### ドロップゾーンの制限
ドロップ可能なゾーンを制限するには、vue.jsのディレクティブを使用します。

```javascript
<template>
  <div id="app">
    <div v-draggable>
      ドラッグ可能な要素
    </div>
    <div v-droppable class="dropzone">
      ドロップ可能なゾーン
    </div>
  </div>
</template>

<script>
export default {
  directives: {
    draggable: {
      bind(el) {
        el.setattribute("draggable", true);

        el.addeventlistener("dragstart", handledragstart);

        function handledragstart(e) {
          e.datatransfer.setdata("text", el.innertext);
        }
      }
    },
    droppable: {
      bind(el) {
        el.addeventlistener("dragenter", handledragenter);
        el.addeventlistener("dragover", handledragover);
        el.addeventlistener("dragleave", handledragleave);
        el.addeventlistener("drop", handledrop);

        function handledragenter(e) {
          e.preventdefault();
          el.classlist.add("active");
        }

        function handledragover(e) {
          e.preventdefault();
        }

        function handledragleave() {
          el.classlist.remove("active");
        }

        function handledrop(e) {
          e.preventdefault();
          const data = e.datatransfer.getdata("text");
          el.innertext = data;
          el.classlist.remove("active");
        }
      }
    }
  }
};
</script>

<style>
#app {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

div {
  padding: 20px;
  border: 1px solid #333;
}

.dropzone {
  background-color: #f2f2f2;
}

.active {
	background-color: #ccc;
}
</style>
```

上記のコードでは、`v-droppable`ディレクティブを使用してドロップ可能なゾーンを制限しています。`v-draggable`ディレクティブを使用してドラッグ可能な要素の実装を行っています。

### 受け入れ条件の実装
特定の条件を満たす要素のみをドロップできるようにするには、ドロップイベントの中で条件を判定し、不要な要素のドロップを防ぐことができます。

```javascript
<template>
  <div id="app">
    <div v-draggable>
      ドラッグ可能な要素
    </div>
    <div v-droppable class="dropzone" @drop="handledrop">
      ドロップ可能なゾーン
    </div>
  </div>
</template>

<script>
export default {
  directives: {
    draggable: {
      bind(el) {
        el.setattribute("draggable", true);

        el.addeventlistener("dragstart", handledragstart);

        function handledragstart(e) {
          e.datatransfer.setdata("text", el.innertext);
        }
      }
    },
    droppable: {
      bind(el) {
        el.addeventlistener("dragenter", handledragenter);
        el.addeventlistener("dragover", handledragover);
        el.addeventlistener("dragleave", handledragleave);

        function handledragenter(e) {
          e.preventdefault();
          el.classlist.add("active");
        }

        function handledragover(e) {
          e.preventdefault();
        }

        function handledragleave() {
          el.classlist.remove("active");
        }
      }
    }
  },
  methods: {
    handledrop(e) {
      e.preventdefault();
      const data = e.datatransfer.getdata("text");

      if (data === "ドラッグ可能な要素") {
        this.$refs.droppable.innertext = data;
        this.$refs.droppable.classlist.remove("active");




## 【Vue.js】関連のまとめ
https://hack-note.com/summary/vuejs-summary/



## オンラインスクールを講師として活用する！
https://hack-note.com/programming-schools/



## 0円でプログラミングを学ぶという選択
- [techacademyの無料体験](//af.moshimo.com/af/c/click?a_id=2612475&amp;p_id=1555&amp;pc_id=2816&amp;pl_id=22706&amp;url=https%3a%2f%2ftechacademy.jp%2fhtmlcss-trial%3futm_source%3dmoshimo%26utm_medium%3daffiliate%26utm_campaign%3dtextad)
- [オンラインスクール dmm webcamp pro](//af.moshimo.com/af/c/click?a_id=2612482&amp;p_id=1363&amp;pc_id=2297&amp;pl_id=39999&amp;guid=on)
- [レバテックカレッジ｜大学生向け 無料説明会](//af.moshimo.com/af/c/click?a_id=4071793&p_id=3198&pc_id=7488&pl_id=41848)
