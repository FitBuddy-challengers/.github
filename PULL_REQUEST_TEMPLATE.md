<!--
PR 제목은 아래 섹션이 아니라 GitHub의 Title 입력란에 작성하세요.
예: Feature/#48 Top Bar & Navigation Bar related code refactoring
-->

## 📝 Explanation
PR 상세 내용을 적어주세요.
- TopBar는 파일 이동 위주. 필요 시 develop 브랜치와 추가 머지 고려.
- Bottom Navigation 개편 및 중앙 FAB 추가, Gradient 강조 등.

## ✔️ PR Type
- [x] Code refactoring
- [ ] Add new features
- [ ] Bug fix
- [ ] UI design changes
- [ ] Docs
- [ ] Test (add/refactor)
- [ ] Build/PM
- [ ] File/Folder rename
- [ ] Remove files/folders
- [ ] Other: __________________

## 📎 Related Issue
Closes #48

## 🔍 Summary (by Author)
**NEW**
- 하단 네비게이션 재구성 및 중앙 FAB 도입
- 선택 아이콘에 Gradient 강조 적용

**IMPROVEMENT**
- 탭 전환 및 로그아웃 UI 개선

**REFACTOR**
- Navigation 아이템 타입/상태/콜백 네이밍 정리

**ETC**
- 일부 내부 파일 `.gitignore` 정리

## 🧩 Commits (highlights)
- `B40659F` 🚚 Navigation bar 이름을 `LinkuNavigationBar`로 변경
- `F8F5073` 🚚 `SearchBarTopSheet.kt` 디자인 모듈 `top` 패키지로 이동
- `C73A31A` ✨ `PixelScaler.kt` 추가
- `61C67EF` ✨ `LinkuNavigationBarFab.kt` 추가
- `0ECE249` ⚡️ BottomBar 코드 안정화
- `654b361` ✨ `LinkuNavigationItem.kt` 추가
- `9b30fea` 💡 `PixelScaler.kt` 주석 보강
- `0b613f7` ✨ `GradientTint.kt` 추가
> 실제 커밋 해시/메시지는 GitHub가 자동 표기합니다. 위 목록은 하이라이트 예시입니다.

## 🗂 Changes Cohort / File(s) Summary
**Navigation 상태/라우팅 업데이트**
- `app/.../MainApp.kt` : `LinkuNavigationItem` 교체, route 매핑/타입 정리, `onFabClick` 추가, 딥링크 파싱 보완

**신규 Bottom Bar 컴포넌트 도입 / 기존 제거**
- `app/.../component/LinkuNavigationBar.kt`
- `app/.../component/LinkuNavigationBarFab.kt`
- `design/.../modifier/GradientTint.kt`
- (기존 `navigationBar`/`navigationItem` 및 관련 preview/constant 제거)

**Design Search 컴포넌트 패키지 이동**
- `design/.../top/search/SearchBarTopSheet.kt`
- `design/.../SearchSheetHost.kt` (import 정리)

**FastSearchItem 경로 반영**
- `feature-curation/.../CurationViewModel.kt`
- `feature-file/.../FileViewModel.kt`
- `feature-home/.../HomeViewModel.kt`  
  → `com.example.design.top.search.fastsearchitem` import로 통일

**레이아웃 사이징 조정**
- `feature-file/.../FileSearchBar.kt` : `width=360.dp` → `fillMaxWidth()`, `height=48.dp`

**유틸 추가**
- `design/.../util/PixelScaler.kt` : `dp` / `TextUnit` 확장 등

**기타**
- `app/.../Splash.kt`, `.gitignore` 정리 등

## ✅ Checklist (Done criteria)
- [ ] 불필요한 리컴포지션 구간 제거
- [ ] 신규 네비 컴포넌트에서 기존 기능 동등 동작(E2E)
- [ ] 단위 테스트(아이템 선택/라우팅) 추가
- [ ] 문서화(폴더 구조/네이밍/DI 흐름) 반영

## 🧪 Test Notes
- [ ] 하단 탭 전환 시 프레임 드롭(>16ms) 기존 대비 **N% 감소**
- [ ] 파일 화면 검색바 포커스/IME 동작 확인(회전/다크모드)

## 🖼 Screenshots / Demo
<!-- 필요 시 이미지/GIF 첨부 -->

## 🔙 Rollback Plan
- 이슈 발생 시 `vX.Y` 태그로 롤백
- 필요 시 기존 `navigationBar` 플래그 재활성화

---

<!-- (옵션) PR 상단 요약 카드가 필요할 때 붙여넣기 -->
<details>
<summary>PR Summary Table (optional)</summary>

| Status | Title/No. | Author | Base ← Head | Merged | Commits | Checks | Files |
|--------|-----------|--------|-------------|--------|---------|--------|-------|
| MERGED | Feature/#48 Top Bar & Navigation Bar related code refactoring #51 | KateteDeveloper | develop ← feature/#48 | 17 hours ago | 11 | 0 | 19 |

</details>

<!-- (옵션) 시퀀스 다이어그램: PR 본문에서 바로 렌더링됩니다. -->
<details>
<summary>Mermaid Sequence Diagram (optional)</summary>

```mermaid
sequenceDiagram
    participant U as User
    participant App as MainApp
    participant Nav as LinkuNavigationBar
    participant VM as HomeViewModel
    participant R as Router

    U->>Nav: 탭 아이템 탭(Feeds)
    Nav->>App: onNavClick(item=Feeds)
    App->>R: navigate("/feeds")
    R-->>VM: onRouteChanged("/feeds")
    VM-->>App: UiState(feeds, selected=Feeds)
    App-->>Nav: props { selected=Feeds, badge=... }

    U->>Nav: 중앙 FAB 클릭
    Nav->>App: onFabClick()
    App->>R: navigate("/quick-link")
