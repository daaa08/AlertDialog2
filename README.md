# Dialog2

- edit alert
```java
 public void editAlertShow(){
        final EditText editText = new EditText(this);   // editText 삽입

        AlertDialog.Builder builder = new AlertDialog.Builder(this);
        builder.setTitle("Edit AlertDialog");
        builder.setMessage("blah~blah~");
        builder.setView(editText);
        builder.setPositiveButton("입력" , new DialogInterface.OnClickListener() {
            @Override
            public void onClick(DialogInterface dialogInterface, int i) {
                Toast.makeText(getApplicationContext(),editText.getText().toString(),Toast.LENGTH_SHORT).show(); // text값 받아서 로그 남김

            }
        });
        builder.setNegativeButton("취소", new DialogInterface.OnClickListener() {
            @Override
            public void onClick(DialogInterface dialogInterface, int i) {
                dialogInterface.dismiss();  // 닫기
            }
        });
        builder.setNeutralButton("나중에", new DialogInterface.OnClickListener() {
            @Override
            public void onClick(DialogInterface dialogInterface, int i) {
                dialogInterface.dismiss();
            }
        });
        builder.show(); // alert 창 띄우기
    }
```

- multiple alert
```java
  public void multiAlertShow(){
        final List<String> ListItems = new ArrayList<>();
        ListItems.add("딸기");
        ListItems.add("사과");
        ListItems.add("복숭아");
        ListItems.add("귤");
        final CharSequence[] items =  ListItems.toArray(new String[ ListItems.size()]);

        final List SelectedItems = new ArrayList();

        AlertDialog.Builder builder = new AlertDialog.Builder(this);
        builder.setTitle("Multiple AlertDialog");
        builder.setMultiChoiceItems(items, null, new DialogInterface.OnMultiChoiceClickListener() {
            @Override
            public void onClick(DialogInterface dialogInterface, int i, boolean isChecked) {
                if(isChecked){  // 사용자가 체크한 경우 리스트에 추가
                    SelectedItems.add(i);
                } else if(SelectedItems.contains(i)){  // 이미 리스트에 있는 경우에는 삭제
                    SelectedItems.remove(Integer.valueOf(i)); // 문자열 변환
                }
            }
        });
        builder.setPositiveButton("Yes", new DialogInterface.OnClickListener() {
            @Override
            public void onClick(DialogInterface dialogInterface, int i) {
                String msg = "";
                for(int n =0; n < SelectedItems.size(); n ++ ){
                    int index = (int)SelectedItems.get(n);
                    msg = msg + "\n" + (n+1) + " : " + ListItems.get(index);
                    Toast.makeText(getApplicationContext(),
                            "Total "+ SelectedItems.size() +" Items Selected.\n"+ msg , Toast.LENGTH_LONG)
                            .show();
                }
            }
        });
        builder.setNegativeButton("No", new DialogInterface.OnClickListener() {
            @Override
            public void onClick(DialogInterface dialogInterface, int i) {
                dialogInterface.dismiss();
            }
        });
        builder.show();
    }

```

- custom alert
```java
    public void loginAlertShow(){
        AlertDialog.Builder builder = new AlertDialog.Builder(this);
        LayoutInflater inflater = getLayoutInflater();  // fragment 안의 레이아웃 호출
        View view = inflater.inflate(R.layout.dialog_login, null);
        builder.setView(view);
        final EditText email = view.findViewById(R.id.editEmail);
        final EditText password =  view.findViewById(R.id.editPs);

        builder.setPositiveButton("확인", new DialogInterface.OnClickListener() {
            @Override
            public void onClick(DialogInterface dialogInterface, int i) {
                String strEmail = email.getText().toString();
                String strPs = password.getText().toString();
                Toast.makeText(getApplicationContext(),strEmail+"/"+strPs,Toast.LENGTH_SHORT).show();
            }
        });

        builder.setNegativeButton("닫기", new DialogInterface.OnClickListener() {
            @Override
            public void onClick(DialogInterface dialogInterface, int i) {
                dialogInterface.dismiss();
            }
        });
        builder.show();
    }
```
