# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 프로젝트 개요

이 프로젝트는 Think Ultra 기법을 Sequential Thinking MCP 도구에 통합하는 작업을 진행 중입니다. 현재 Dummy folder는 주로 실험 및 개발 작업을 위한 공간으로 사용되고 있습니다.

## MCP 관련 도구 및 설정

### Sequential Thinking MCP
- Docker 기반으로 실행: `docker run -i --rm mcp/sequentialthinking`
- 구조화된 단계별 추론을 지원하는 MCP 도구
- Think Ultra 기법 통합을 통해 고급 추론 기능 추가 예정

### Memory Bank 설정
- 경로: `/Users/hyoch/MCP_folder/Memory-bank`
- 프로젝트별 메모리 뱅크를 통해 컨텍스트 관리

## 주요 작업 디렉토리

- `/Users/hyoch/Dummy folder`: 현재 작업 디렉토리
- `/Users/hyoch/MCP_folder`: MCP 관련 파일 및 Memory Bank 저장소
- `/Users/hyoch/Documents/Hyos_SecondBrain`: Obsidian 기반 문서 저장소 (Sequential Thinking MCP 가이드 포함)

## 개발 시 주의사항

1. **Think Ultra 통합 작업**
   - Serial/Parallel Test-Time Compute 구현
   - Budget-Forcing Method 적용
   - Meta-Reasoning 및 Self-Correction 기능 통합

2. **MCP 도구 사용**
   - Docker 컨테이너로 실행되는 MCP 도구들의 설정은 `~/.claude.json`에서 관리
   - Sequential Thinking MCP는 stdio 통신 사용

3. **문서 참조**
   - Think Ultra 통합 가이드: Obsidian vault의 관련 문서 참조
   - Slow Think 기법과의 연계 방안