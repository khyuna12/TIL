## Branch

- **독립적**인 작업흐름을 만들고 관리

<br>

## merge

- 각 브랜치에서 작업한 후 이력을 합칠 때
- 동일한 파일을 수정한 경우(다른 파일 수정한 경우 충돌없이 자동으로 Merge commit 생성됨)

```
git merge <브랜치 이름>
```

- **merge - fast foward** : 브랜치에 변경사항 없을 경우 브랜치로 이동 후 commit, main branch로 병합

- **merge - merge commit** : 브랜치에 변경사항 있을 경우 브랜치로 이동 후 commit, main branch commit, main branch로 병합

<br>

---

<br>

1. **브랜치 생성**

```
git branch <브랜치 이름>
```

<br>

2. **브랜치 이동(switch)**

```
git checkout <브랜치 이름>
```

<br>

3. 브랜치 생성 및 이동

```
git checkout -b <브랜치 이름>
```

<br>

4. 브랜치 목록

```
git branch
```

<br>

5. 브랜치 삭제

```
git branch -d <브랜치 이름>
```

<br>
