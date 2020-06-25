## branch
* branch 원격 포함하여 전체 조회

``` 
git branch -a 
```   
* branch 생성
```
git checkout -b feature-edit_button  
git push origin feature_edit_button  
git branch --set-upstream-to origin/feature_edit_button  //remote branch에도 생성
git branch -a  
```
* branch 이동
```
git checkout 브랜치명
```
* branch 삭제
```
git branch -d feature_frontend_table  
git push origin :feature_frontend_table  
git remote update  
git remote prune origin // remote branch update
```


## merge
* dev브랜치와 병합

```
git checkout dev
git pull
git branch feature_branch
git push
```
