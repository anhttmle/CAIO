---
name: commit-code
description: >-
  Tạo git commit an toàn theo chuẩn dự án NIX. Dùng khi user nói "commit",
  "commit code", "tạo commit", hoặc yêu cầu lưu thay đổi vào git. Chỉ chạy
  khi user yêu cầu rõ — không commit chủ động.
---

# Commit Code

## Khi nào chạy

- User **yêu cầu rõ** commit (ví dụ: "commit current code", "commit đi").
- Nếu không rõ user có muốn commit hay không → **hỏi trước**.

**Không** commit khi chỉ implement xong task, trừ khi user bảo commit.

---

## Git safety (bắt buộc)

- **Không** `git config` (global hoặc local).
- **Không** lệnh phá huỷ: `push --force`, `reset --hard`, v.v. (trừ khi user yêu cầu rõ).
- **Không** `--no-verify` / `--no-gpg-sign` trừ khi user yêu cầu.
- **Không** `push` trừ khi user yêu cầu.
- **Không** lệnh interactive (`git add -i`, `git rebase -i`).
- **Không** commit file secrets (`.env`, credentials, keys).

### Amend — chỉ khi đủ cả 3

1. User yêu cầu amend, **hoặc** hook sửa file sau commit thành công.
2. HEAD commit do **agent tạo trong session này**.
3. Commit **chưa push** lên remote.

Nếu commit **fail** / bị hook reject → sửa lỗi, tạo **commit mới** (không amend).

---

## Workflow

### 1. Thu thập (chạy song song)

```bash
git status
git diff
git diff --cached
git log -5 --oneline
```

Nếu commit trên branch đã có remote: kiểm tra ahead/behind (không push trừ khi được yêu cầu).

### 2. Phân tích

- Xem **toàn bộ** thay đổi sẽ vào commit (staged + cần stage).
- Cảnh báo nếu có file nhạy cảm.
- Draft message 1–2 câu, focus **why** not what.
- Theo style repo gần đây (`feat:`, `fix:`, `docs:` …).

### 3. Commit (tuần tự)

```bash
git add <paths-cần-thiết>
git commit -m "$(cat <<'EOF'
<subject line>

<body optional — complete sentences>
EOF
)"
git status
```

- Không commit rỗng.
- Chỉ add file liên quan request.
- Message qua HEREDOC (giữ format đúng).

### 4. Hook fail

Sửa lỗi hook → **commit mới**, không amend (trừ khi đủ điều kiện amend ở trên).

---

## Message guide (NIX)

| Prefix | Khi nào |
|--------|---------|
| `feat:` | Tính năng mới |
| `fix:` | Sửa bug |
| `docs:` | Spec, AGENT, ONBOARDING |
| `refactor:` | Đổi cấu trúc, không đổi hành vi |
| `test:` | Chỉ test |

Ví dụ:

```
fix(user_app): reconcile stale session on iOS Keychain reinstall

Clear tokens when JWT exists but available_mobile_roles is empty.
```

---

## Sau commit

- Báo hash + message tóm tắt.
- `git status` phải clean (hoặc nêu file còn lại chưa commit).
- **Không** push trừ khi user yêu cầu.

## Không làm trong skill này

- Tạo PR (dùng workflow `gh pr create` riêng khi user yêu cầu).
- `git push` / force push.
- Sửa code ngoài việc fix hook reject.
