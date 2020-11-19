Unity中的有些对象的属性不是公开的，甚至不是c#端的，通过c#的反射是反射不出来的属性。
通过SerializedObject的方式，可也获取未公开属性。
在不知道属性的名称时，可以通过GetIterator遍历属性，来获取所有属性名称。注意第一个Iterator的要Next(true)
再找到需要的属性，再调用FindProperty获取具体的属性。
示例：
    public static void GetShaderImporterTextureNames(ShaderImporter shaderImporter,ref List<string> names)
    {
        var so = new SerializedObject(shaderImporter);
        var defaultTextures = so.FindProperty("m_DefaultTextures");

        for (int i = defaultTextures.arraySize - 1; i >= 0; i--)
        {
            var propertyName = defaultTextures.GetArrayElementAtIndex(i).displayName;
            names.Add(propertyName);
        }
    }