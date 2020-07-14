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

* 1.‘develop’ 브랜치에서 새로운 기능에 대한 feature 브랜치를 분기한다.
* 2.새로운 기능에 대한 작업 수행한다.
* 3.작업이 끝나면 ‘develop’ 브랜치로 병합(merge)한다.
* 4.더 이상 필요하지 않은 feature 브랜치는 삭제한다.
* 5.새로운 기능에 대한 ‘feature’ 브랜치를 중앙 원격 저장소에 올린다.(push)
https://gmlwjd9405.github.io/2018/05/11/types-of-git-branch.html
```
// feature 브랜치(feature/login)를 'develop' 브랜치('master' 브랜치에서 따는 것이 아니다!)에서 분기
$ git checkout -b feature/login develop

/* ~ 새로운 기능에 대한 작업 수행 ~ */

/* feature 브랜치에서 모든 작업이 끝나면 */
// 'develop' 브랜치로 이동한다.
$ git checkout develop
// 'develop' 브랜치에 feature/login 브랜치 내용을 병합(merge)한다.
# --no-ff 옵션: 아래에 추가 설명
$ git merge --no-ff feature/login
// -d 옵션: feature/login에 해당하는 브랜치를 삭제한다.
$ git branch -d feature/login
// 'develop' 브랜치를 원격 중앙 저장소에 올린다.
$ git push origin develop
https://gmlwjd9405.github.io/2018/05/11/types-of-git-branch.html
```
