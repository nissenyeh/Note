## REST framework

### 基本

- 可以方便地做API
- 用基本的viewsets, ModelSerializer建構API


### ViewSet/ModelViewSet是什麼？

- 取代get(),.post()提供了`list`和`create`（原本DJANGO 只有View類型)

#### ModelViewSet

- Django只提供View
- ModelViewSet是一種類別，繼承自GenericAPIView，GenericAPIView，則繼承自APIView，
- 因為繼承自GenericAPIView，所以要給他queryset 跟serializer_class
- 提供.list(), .retrieve(), .create(), .update(), .partial_update(), and .destroy(). actions. 

```py
class CaseViewSet(viewsets.ModelViewSet) :
   // 
```