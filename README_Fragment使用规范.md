[Fragment]规范
==============================================================================



1:Activity里面放Fragment需要先判断savedInstanceState是否为null 如果不为null在添加新的Fragment

示例代码：

```java
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_personal_center);
    如果savedInstanceState＝＝null肯定是第一次启动 没有其他可能 但是如果不是第一次启动 savedInstanceState一般不出意外都不为null
    if(savedInstanceState==null){
        CustomFragment preFragment=new CustomFragment();
        FragmentTransaction ft=this.getSupportFragmentManager().beginTransaction();
        ft.replace(R.id.ll_content, preFragment，“customTagName”);
        ft.commit();
    }else{
       如果你需要一个当前Fragment的引用 你可以在这里从FragmentManager里面通过以前设置的tag去取
    }
}
```


2：生成View的操作必须放在onCreatView里面执行

示例代码

```java
public View onCreateView(LayoutInflater inflater, ViewGroup container, Bundle savedInstanceState) {
    if(rootView==null){
        ctx = getActivity().getApplicationContext();
        rootView = getActivity().getLayoutInflater().inflate(R.layout.fragment_personal_center, null);
        findViewByid...
        getDataFromNet...
    }else{
        if(rootView.getParent() != null){
            ((ViewGroup) rootView.getParent()).removeView(rootView);
        }
    }
    return rootView;
}
```

