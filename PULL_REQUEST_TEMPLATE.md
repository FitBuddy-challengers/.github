# PR Title
Feature/#48 Top Bar & Navigation Bar related code refactoring

## 📝 Explanation
PR 상세 내용을 적어주세요.
- TopBar는 파일 이동 위주. 필요 시 develop 브랜치와 추가 머지 고려.
- Bottom Navigation 개편 및 FAB 추가, Gradient 강조 등.

## ✔️ PR Type
- [ ] Add new features
- [ ] Bug fix
- [ ] UI design changes (CSS/UI)
- [x] Code refactoring
- [ ] Docs
- [ ] Test (add/refactor)
- [ ] Build/PM
- [ ] File/Folder rename
- [ ] Remove files/folders
- [ ] Other: __________

## 📎 Related Issue
Closes #48

## 🔍 Summary (by author)
**New**
- 하단 네비게이션 개편 및 중앙 FAB 도입
- 선택 아이콘 Gradient 강조

**Improvement**
- 파일 화면 검색바 고정폭 → 가변(가로 전체), 가독성/사용성 개선
- 탭 전환/로그아웃 UI 개선

**Refactor**
- Navigation item 타입/상태/콜백 네이밍 정리

**Etc**
- 일부 내부 파일 .gitignore 정리

## 🧩 Commits (highlights)
- `B40659F` 🚚 Navigation bar 이름을 `LinkuNavigationBar`로 변경
- `F8F5073` 🚚 `SearchBarTopSheet.kt` 디자인 모듈 `top` 패키지로 이동
- `C73A31A` ✨ `PixelScaler.kt` 추가
- `61C67EF` ✨ `LinkuNavigationBarFab.kt` 추가
- `0ECE249` ⚡️ BottomBar 코드 안정화
- `654b361` ✨ `LinkuNavigationItem.kt` 추가
- `F40DB2D` ✨ `LinkuNavigationItem.kt` (정리)
- `9b30fea` 💡 `PixelScaler.kt` 주석 보강
- `0b613f7` ✨ `GradientTint.kt` 추가
- `8348655` 💡 네비게이션 관련 코드 리팩토링
> *실제 커밋 해시/메시지는 GitHub가 자동으로 표시합니다. 위 목록은 하이라이트 가이드입니다.*

## 🗂 Changes Cohort / File(s) Summary
**Navigation 상태/라우팅 업데이트**
- `App/.../MainApp.kt` : `LinkuNavigationItem` 교체, route 매핑/타입 정리, `onFabClick` 추가, 딥링크 파싱 보완

**신규 Bottom Bar 컴포넌트 도입/기존 제거**
- `App/.../component/LinkuNavigationBar.kt`
- `App/.../component/LinkuNavigationBarFab.kt`
- `design/.../modifier/GradientTint.kt`
- (기존 `navigationBar`/`navigationItem` 및 관련 preview/constant 제거)

**Design Search 컴포넌트 패키지 이동**
- `design/.../top/search/SearchBarTopSheet.kt`
- `design/.../SearchSheetHost.kt` (import 정리)

**FastSearchItem 경로 반영**
- `feature-curation/.../CurationViewModel.kt`
- `feature-file/.../FileViewModel.kt`
- `feature-home/.../HomeViewModel.kt`  
  → `com.example.design.top.search.fastsearchitem` import로 변경

**레이아웃 사이징 조정**
- `feature-file/.../FileSearchBar.kt` : `width=360dp` → `fillMaxWidth()`, `height=48.dp`

**유틸 추가**
- `design/.../util/PixelScaler.kt` : `dp`/`TextUnit` 확장 등

**기타**
- `app/.../Splash.kt`, `.gitignore` 정리 등

## ✅ Checklist
- [ ] 앱 부팅~하단탭 전환까지 Recomposition 불필요 구간 제거
- [ ] 새 네비 컴포넌트에서 기존 기능 동등 동작(E2E)
- [ ] 단위 테스트(아이템 선택/라우팅) 추가
- [ ] 문서화(폴더 구조/네이밍/DI 흐름) 반영

## 🧪 Test Notes
- [ ] 하단탭 전환 시 프레임 드랍(>16ms) 기존 대비 **N% 감소**
- [ ] 파일 화면 검색바 포커스/IME 동작 확인(회전/다크모드)

## 🖼 Screenshots / Demo
> 필요 시 이미지/GIF 첨부

## 🔙 Rollback Plan
- 리스크 발생 시 `vX.Y` 태그로 롤백 및 기존 `navigationBar` 플래그 재활성화
