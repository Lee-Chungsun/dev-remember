## [JSP] Table check 접근

###### 이번 글은 jsp 에서 <Tabel>  form에서 checkbox를 생성하고 체크된 tr들의 컬럼 인 td까지 가져 오는 것을 다룰 예정!

###### 진짜 JSP를 5년인가,, 6년만에 해봐서 check된 Row에 접근하고,, td 값에 접근하는 것이 쉽지가 않았는데 막상 해보고 나니 뭐 그냥 간단했다,,

###### 절차는 간단하다.

1. checkbox가 있는 Table 생성
2. name이 checkbox 인 태그에서 checked인 tr들 조회
3. tr에서 td 접근 



### Table

```jsp
<table name="dataTable">
    <tr>
        <thead>
    		<td><input type='checkbox' name='chkAll' onclick='chkChange(this);'></td>
			<td>Acolumn</td>
			<td>Bcolumn</td>
	    </thead>
    </tr>
    <tr>
        <tbody>
            <input type='checkbox' name='chkProc' value=''/>
            <td>Adata</td>
            <td>Bdata</td>
        </tbody>
	</tr>
</table>
```

###### 이런 테이블이 생성되어 있다. 엄청 간단하게 만들어진 Table ,,;;ㅎㅎ 

###### 위의 tr은 head로 checkbox name이 'chkAll'이고 아래의 body row는 name이 'chkProc' 로 서로 다르게 지정해줘야 name으로 가져올 떄 head는 제외하고 가져온다.

###### 다음은 script에서 가져와본다

###### script는 <head></head> 안에 구현해 놓았다

### Script

```jsp
<script	type="text/javascript">
	function reqSubscriptReg()	{
        var colArr = new Array();
		var rowArr = new Array();
        
        // chkProc가 checked인 모든 checkbox를 가져온다 (배열 상태로 가져옴)
        var checkbox = $("input[name=chkProc]:checked");
        
        // 가져온 배열 checkbox로 for문을 실행한다
        checkbox.each(function(i) {
			// checkbox.parent().parent() -> checkbox의 부모(td)의 부모(tr)
			var tr = checkbox.parent().parent().eq(i);
			var td = tr.children();
            
            // eq(0)은 checkbox의 idx
            var adata = td.eq(1).text(); // Adata
			var bdata = td.eq(2).text(); // Bdata
            
            colArr.push(adata);
            colArr.push(bdata);
            
            rowArr.push(rowData)
        }
    }
</script>
```

###### 이렇게 모든 tr의 td로 접근할 수 있다. 

###### 다음은 모든 에 접근해보자. 방식은 동일하나 tr을 배열로 가져온다

```jsp
<script	type="text/javascript">
	function reqSubscriptReg()	{
        var colArr = new Array();
		var rowArr = new Array();
        
        // id가 dataTable 인 table의 tbody의 tr을 가져온다
        var bodySize = $("#dataTable tbody tr");
        
        // 가져온 배열 tr로 for문을 실행한다
        bodySize.each(function(i) {
			// i번째 tr을 가져온다.
			var tr = bodySize.eq(i);
			var td = tr.children();
            
            // eq(0)은 checkbox의 idx
            var adata = td.eq(1).text(); // Adata
			var bdata = td.eq(2).text(); // Bdata
            
            colArr.push(adata);
            colArr.push(bdata);
            
            rowArr.push(rowData)
        }
    }
</script>
```



### 마치며

###### 각 태그마다 id와 child, perant 가 있기 때문에 어떤 태그든 간단하게 접근 할 수 있는 것 같다. 너어어어무 오랜만에 하니까 이런 간단한 것들도 조금 버거웠던 느낌.. jsp 싫었는데 재밌는 것 같기도..?