# OpenFOAM学习

1. OpenFOAM代码执行

进入OpenFOAM的环境之后，比如执行例题incompressible/icoFoam当中的Cavity，时

```
blockMesh //生成网格
icoFoam //直接执行icoFoam的代码文件，调用当前文件夹下面的设置文件
```

```
icoFoam>log.txt& //可以将输出放在txt文件当中
```
```
./Allrun //可以利用已经写好的bash文件直接执行default的一些操作
```

2. OpenFOAM 代码理解

fvcDiv文件中有如下模版函数
```
template<class Type>
tmp<GeometricField<Type, fvPatchField, volMesh>>
div
(
    const GeometricField<Type, fvsPatchField, surfaceMesh>& ssf
)
{
    return tmp<GeometricField<Type, fvPatchField, volMesh>>
    (
        new GeometricField<Type, fvPatchField, volMesh>
        (
            "div("+ssf.name()+')',
            fvc::surfaceIntegrate(ssf)
        )
    );
}
```
函数名为div，对应的返回值类型是tmp<GeometricField<Type, fvPatchField, volMesh>>， 与return部分的返回值类型一致，div函数中的参数列表只有GeometricField<Type, fvsPatchField, surfaceMesh>& ssf
