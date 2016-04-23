###### 個人自製簡易教學，僅提及其中幾種基本功能使用

---

# Simple Git Tutorial

---
## Git 指令
- `git init`: 將當前資料夾設定成本地repository
- `git add file`: 將file加入到待提交區域
- `git commit -m "message"`: 將待提交區域檔案提交出去並附上提交訊息(message)
- `git remote -v`: 顯示遠端repository詳細資訊
- `git remote add nickname https://github.com/username/repositoryname.git`: 將遠端repository加入列表中
- `git pull --rebase nickname master`: 將遠端repository(nickname)的master分支拉至本地repository
- `git push nickname master`: 將本地repository推至遠端repository(nickname)的master分支

---
## 與遠端(github)repository同步
- 1. 首先在遠端開一個新的repository
- 2. 在本地新增一個相同名字的資料夾
- 3. 進入資料夾後使用`git init`
- 4. 使用`git remote add`將遠端repository位址加入
- 5. 使用`git pull`將遠端repository同步至資料夾內
- 6. 之後就可以在資料夾內進行程式碼撰寫，並使用`git add`、`git commit`來進行版本控制
- 7. 在commit完成後，使用`git push`將本地repository同步至遠端repository



