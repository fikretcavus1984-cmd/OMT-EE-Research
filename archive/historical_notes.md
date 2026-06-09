# Historical Notes - OMT-EE Research Archive

## Project Evolution

### Genesis
OMT-EE (Open Media Transport Enhanced Edition) began as an investigation into achieving reliable, high-performance media streaming over network infrastructure. Initial goals were ambitious: stable 4K60 streaming with zero frame drops.

### Early Challenges
The project encountered persistent issues with frame drops occurring irregularly during extended streaming sessions. These drops were particularly frustrating because:
- Network analysis showed no packet loss
- UDP streams were complete and intact
- The problem manifested as application-level timing issues
- Initial debugging efforts focused on wrong layer (network instead of timing)

### Breakthrough: FramePacer Investigation
The critical insight came from examining timing characteristics rather than network packets. It was discovered that frame delivery timing was non-deterministic, causing receiver-side synchronization failures. This led to the FramePacer solution and elimination of frame drops.

### Current Phase: Quality Optimization
With stability achieved, focus shifted to quality enhancement through color format optimization. BGRA/BGRX formats were identified as potential quality improvements, with codec paths verified in both libomtnet and VMX libraries.

---

## Key Findings Summary

### Network Performance
- Safe10G tuning achieved 700+ MB/s sustained throughput
- 4K60 content streaming stable over extended sessions
- 38-minute continuous test with zero frame drops validates network layer
- Network NOT identified as bottleneck for 4K60 resolution

### Timing and Synchronization
- Application-level timing was root cause of initial frame drops
- FramePacer solution eliminated micro-drops through deterministic timing
- Receiver synchronization window: ±2ms tolerance
- System maintains sub-millisecond drift over minutes

### Color Format Support
- BGRA/BGRX paths verified in codec stack
- Potential quality improvement over standard formats
- No additional codec modifications required
- OBS plugin integration remains blocking factor

### Performance Metrics
- Encoding latency: 2-3ms per frame
- Network latency: ~1ms (local network)
- Decoding latency: 1-2ms per frame
- Total end-to-end: 4-6ms (acceptable for live streaming)

---

## Technical Milestones

### Milestone 1: Network Baseline (Completed)
- Established 4K60 streaming capability
- Identified network parameter tuning needs
- Created baseline for performance comparison

### Milestone 2: FramePacer Solution (Completed)
- Diagnosed timing-based frame drop root cause
- Implemented deterministic frame delivery
- Achieved zero-drop operation over 38 minutes

### Milestone 3: Safe10G Tuning (Completed)
- Optimized network parameters
- Validated sustained 700+ MB/s throughput
- Documented configuration for reproducibility

### Milestone 4: Quality Investigation (In Progress)
- Verified BGRA/BGRX codec path support
- Identified OBS plugin as integration blocker
- Planned quality comparison study

### Milestone 5: Production Deployment (Future)
- Integrate BGRA support into OBS plugin
- Complete quality comparison study
- Publish deployment recommendations

---

## Lessons Learned

### 1. Root Cause Analysis Requires Multi-Layer Investigation
- Surface symptoms (frame drops) don't always indicate problem layer
- Network layer looked normal; problem was in application timing
- Lesson: Systematic diagnosis across all layers prevents false conclusions

### 2. Determinism is Critical for Real-Time Systems
- Simple queuing insufficient for real-time performance
- Predictable resource allocation essential
- Lesson: Design with determinism in mind from architecture stage

### 3. Performance Optimization Requires Validation
- Parameter tuning without testing leads to false assumptions
- Extended stress testing (38+ minutes) reveals subtle issues
- Lesson: Comprehensive validation more important than theoretical optimization

### 4. Architecture Decisions Have Long-Term Impact
- Early FramePacer architecture decision avoided complex alternative solutions
- Simplified subsequent tuning work
- Lesson: Invest time in architecture clarity early

### 5. Documentation Enables Future Development
- Detailed findings from each phase enables next phase work
- Clear parameter documentation supports deployment
- Lesson: Document thoroughly as you go; future self will appreciate it

---

## Open Questions & Unknowns

1. **Color Format Quality Impact:** Actual BGRA quality improvement magnitude TBD
2. **Codec Performance:** VMX handling of BGRA vs. NV12 - same or different performance?
3. **Plugin Integration Complexity:** How difficult is OBS plugin format addition?
4. **Latency Implications:** Does BGRA processing add any latency penalty?
5. **Scalability:** How do these parameters perform at 8K resolution?
6. **Future Formats:** What about HDR, ProRes, or other advanced formats?

---

## Related Technologies & Comparisons

### NDI (Network Device Interface)
- **Status:** Industry standard for network streaming
- **Throughput:** ~250 MB/s typical
- **Quality:** Lossless at network speeds
- **Latency:** 2-4ms typical
- **Comparison:** OMT-EE offers superior throughput, better compression

### H.264/H.265 Codecs
- **H.264:** Mature, wide compatibility, good compression
- **H.265:** Better compression, higher latency, less compatible
- **Use in OMT-EE:** Both supported through VMX codec interface

### OBS Project
- **Status:** Open-source broadcast software
- **Integration:** Plugin-based extension model
- **Relevance:** Primary integration point for OMT-EE consumer availability
- **Challenge:** Format support limited to plugin implementation

---

## Archive Notes

This document serves as a record of project evolution, decision points, and accumulated knowledge.

**Last Updated:** 2026-06-09
**Maintained By:** OMT-EE Research Team
**Review Schedule:** Quarterly or upon major milestone completion
