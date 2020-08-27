# Pasar data con Handler y Bundler Android

## Recibir la info con handler

```java

private static final String RESULT = "result";

// La clase Recepciones implementa la clase | public class Recepciones implements Parcelable { ...

private ArrayList<Recepciones> recepciones;

// Receive request
  @SuppressLint("HandlerLeak")
  private Handler handler = new Handler(){
      @Override
      public void handleMessage(Message msg){

          Bundle bundle = msg.getData();
          recepciones = bundle.getParcelableArrayList(RESULT);

          if(getActivity() != null && !getActivity().isFinishing()) {
              manageReception();
          }
      }
  };
  ```
  
  ## Enviar información
  
  ```java
ArrayList<Recepciones> res = new ArrayList<>();

if (objSession.contains("sessionID")) {

    String sID = objSession.getString("sessionID", "");

    DataFetcherV3 objWS = new DataFetcherV3();

    res = objWS.getRecepciones(sID, dateFrom, dateTo);
}

Message msg = handler.obtainMessage();
Bundle bundle = new Bundle();
bundle.putParcelableArrayList(RESULT,res);
msg.setData(bundle);
handler.sendMessage(msg);
```
  
