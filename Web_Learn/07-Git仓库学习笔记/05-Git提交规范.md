

1. feat: 新增功能
2. fix: bug修复
3. docs: 文档更新
4. style: 不影响程序逻辑的代码修改(修改空白字符，格式缩进，补全缺失的分号等，没有改变代码逻辑)
5. refactor: 重构代码(既没有新增功能，也没有修复bug)
6. perf: 性能，体验优化
7. test: 新增测试用例或是更新现有测试
8. build: 主要目的是修改项目构建系统(例如 glup, rollback, rollup 的配置等)的提交
9. ci: 主要目的是修改项目继续集成流程(例如 Travis, Jenkins, GitLab CI, Circle等)的提交
10. chore: 不属于以上类型的其他类，比如构建流程，依赖管理
11. revert: 回滚某个更早之前的提交



1. **feat**：新增功能（Feature）
2. **fix**：修复缺陷（Bug Fix）
3. **docs**：文档更新（Documentation）
4. **style**：代码格式（不影响代码运行的变动，如空格、缩进、缺少分号等）
5. **refactor**：重构代码（既没有新增功能，也没有修复缺陷）
6. **perf**：性能优化（Performance Improvement）
7. **test**：添加测试（Test）
8. **build**：构建系统或外部依赖的变动（Build System, Dependencies）
9. **ci**：持续集成配置变动（Continuous Integration）
10. **chore**：其他不修改src或测试文件的变动（如构建流程、依赖管理等）
11. **revert**：回滚到上一个提交（Revert）
12. **merge**：合并分支（Merge，通常由Git自动生成）
13. **arch**：架构级别的变动（Architecture）
14. **security**：安全修复（Security Fix）
15. **deprecate**：弃用功能（Deprecation）

这些动词通常与提交信息的前缀一起使用，例如：

- `feat: 添加新功能`
- `fix: 修复登录页面的bug`
- `docs: 更新README文件`
- `style: 格式化代码，增加空格`
- `refactor: 重构用户认证流程`
- `perf: 优化数据库查询`
- `test: 为登录功能添加单元测试`
- `build: 更新Webpack配置`
- `ci: 配置Travis CI`
- `chore: 更新依赖到最新版本`
- `revert: 回滚到之前的提交`
- `merge: 合并来自feature-branch的更改`
- `arch: 重构项目架构`
- `security: 修复安全漏洞`
- `deprecate: 弃用旧的API端点`