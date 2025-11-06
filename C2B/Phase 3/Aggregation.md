# 1. Overview

## 1.1 Introduction & Purpose
> Use File/Folder tree

## 1.2 File & Directory Structure
> Link to detail of JCL, COBOL, COPY // (2.1) | (2.2) | (2.3)

## 1.3 System Architecture & Key Components
> PERFORM/CALL among COBOL files to COBOL/COPY -> draw by engineer, zoom-in by file-context + sub-graph (node, k-hop neighbor)

## 1.4 Overall Data Flow
> Parsing I/O for each file -> draw by engineer, zoom-in by file-context + sub-graph (node, k-hop neighbor)

## 1.5 Overall Control Flow 
> Parsing JCL control flow -> draw by engineer // (2.3)
- 1.5.1 <JCL 001> Diagram
  > draw by engineer, zoom-in by file-context + sub-graph (node, k-hop neighbor) 
- 1.5.2 <JCL 002> Diagram 
  > draw by engineer, zoom-in by file-context + sub-graph (node, k-hop neighbor) 
- 1.5.3 ...

# 2. Detail Source code 
> Will be children of (1)
## 2.1 <File 001> (COBOL)
- 2.1.1 Metadata
- 2.1.2 Program Structure Highlights
- 2.1.3 Data Flow
- 2.1.4 Control Flow
- 2.1.5 Interactions

## 2.2 <File 002> (COPY)
- 2.2.1 Metadata
- 2.2.2 Program Structure Highlights
- 2.2.3 Data Flow
- 2.2.4 Control Flow
- 2.2.5 Interactions

## 2.3 <File 003> (JCL, shell)
- 2.3.1 Summary
- 2.3.2 Metadata Content
- 2.3.3 Dependency
- 2.3.4 Business Process
