---
title: "PyPy compilation result"
---

python

```
import pypyjit
import pprint


def f(jitLoopInfo):
    for op in jitLoopInfo.operations:
        print(op)


pypyjit.set_compile_hook(f)


def g(x):
    return x + 234


ret = 0
for i in range(2000):
    ret = g(ret)
```


result

```
i1 = getfield_gc_i(p0, descr=<FieldS pypy.interpreter.pyframe.PyFrame.inst_last_instr 40>)
p2 = getfield_gc_r(p0, descr=<FieldP pypy.interpreter.pyframe.PyFrame.inst_pycode 64>)
i3 = getfield_gc_i(p0, descr=<FieldS pypy.interpreter.pyframe.PyFrame.inst_valuestackdepth 72>)
p4 = getfield_gc_r(p0, descr=<FieldP pypy.interpreter.pyframe.PyFrame.inst_debugdata 16>)
p5 = getfield_gc_r(p0, descr=<FieldP pypy.interpreter.pyframe.PyFrame.inst_lastblock 48>)
p6 = getfield_gc_r(p0, descr=<FieldP pypy.interpreter.pyframe.PyFrame.inst_locals_cells_stack_w 56>)
p8 = getarrayitem_gc_r(p6, 0, descr=<ArrayP 8>)
p10 = getarrayitem_gc_r(p6, 1, descr=<ArrayP 8>)
p12 = getarrayitem_gc_r(p6, 2, descr=<ArrayP 8>)
label(p0, p13, i1, p2, i3, p4, p5, p8, p10, p12, descr=TargetToken(4429777600))
debug_merge_point(0, 0, '(pypyjit: get_printable_location disabled. no debug_print)')
guard_value(i3, 1, descr=<Guard0x10809a500>) [p0, i1, p2, i3, p4, p5, p8, p10, p12, p13]
guard_nonnull(p4, descr=<Guard0x1080a22f0>) [p0, i1, p2, i3, p4, p5, p8, p10, p12, p13]
p15 = getfield_gc_r(p4, descr=<FieldP pypy.interpreter.pyframe.FrameDebugData.inst_w_f_trace 48>)
guard_isnull(p15, descr=<Guard0x1080a2338>) [p0, i1, p2, i3, p4, p5, p8, p10, p12, p13]
guard_class(p8, 4404983760, descr=<Guard0x1080a2650>) [p0, i1, p2, i3, p4, p5, p8, p10, p12, p13]
i17 = getfield_gc_i(p8, descr=<FieldS pypy.module.__builtin__.functional.W_IntRangeIterator.inst_current 8>)
i18 = getfield_gc_i(p8, descr=<FieldS pypy.module.__builtin__.functional.W_IntRangeOneArgIterator.inst_stop 32 pure>)
i19 = int_lt(i17, i18)
guard_true(i19, descr=<Guard0x1080a2608>) [p0, i1, p2, i3, p4, p5, p8, p10, p12, p13]
i21 = int_add(i17, 1)
i22 = getfield_gc_i(p4, descr=<FieldU pypy.interpreter.pyframe.FrameDebugData.inst_is_being_profiled 74>)
setfield_gc(p8, i21, descr=<FieldS pypy.module.__builtin__.functional.W_IntRangeIterator.inst_current 8>)
guard_value(i22, 0, descr=<Guard0x10809ab00>) [p0, p2, p4, p5, p8, p12, i22, p13, i17]
debug_merge_point(0, 0, '(pypyjit: get_printable_location disabled. no debug_print)')
guard_value(p2, ConstPtr(ptr24), descr=<Guard0x1080a25c0>) [p0, p2, p4, p5, p8, p12, i22, p13, i17]
p25 = getfield_gc_r(p4, descr=<FieldP pypy.interpreter.pyframe.FrameDebugData.inst_w_locals 64>)
guard_value(p25, ConstPtr(ptr26), descr=<Guard0x10809ab60>) [p0, p2, p4, p5, p8, p12, i22, p13, i17]
guard_not_invalidated(descr=<Guard0x1080a2578>) [p0, p2, p4, p5, p8, p12, i22, p13, i17]
p27 = getfield_gc_r(p25, descr=<FieldP pypy.objspace.std.dictmultiobject.W_ModuleDictObject.inst_mstrategy 16 pure>)
guard_value(p27, ConstPtr(ptr28), descr=<Guard0x10809aaa0>) [p0, p2, p4, p5, p8, p12, i22, p13, i17]
debug_merge_point(0, 0, '(pypyjit: get_printable_location disabled. no debug_print)')
p29 = getfield_gc_r(p4, descr=<FieldP pypy.interpreter.pyframe.FrameDebugData.inst_w_globals 56>)
setfield_gc(ConstPtr(ptr30), i17, descr=<FieldS pypy.objspace.std.typeobject.IntMutableCell.inst_intvalue 8>)
i32 = instance_ptr_eq(ConstPtr(ptr31), p29)
guard_true(i32, descr=<Guard0x10809aa40>) [p0, p4, p5, p8, p12, p13, i32, None]
guard_value(p29, ConstPtr(ptr34), descr=<Guard0x10809a9e0>) [p0, p4, p5, p8, p12, p13, i32, None]
p35 = getfield_gc_r(p29, descr=<FieldP pypy.objspace.std.dictmultiobject.W_ModuleDictObject.inst_mstrategy 16 pure>)
guard_value(p35, ConstPtr(ptr36), descr=<Guard0x10809a980>) [p0, p4, p5, p8, p12, p13, i32, None]
debug_merge_point(0, 0, '(pypyjit: get_printable_location disabled. no debug_print)')
i38 = getfield_gc_i(ConstPtr(ptr37), descr=<FieldS pypy.objspace.std.typeobject.IntMutableCell.inst_intvalue 8>)
debug_merge_point(0, 0, '(pypyjit: get_printable_location disabled. no debug_print)')
p41 = call_r(ConstClass(_ll_1_threadlocalref_get__Ptr_GcStruct_objectLlT_Signed), 64, descr=<Callr 8 i EF=1 OS=5>)
p42 = getfield_gc_r(p41, descr=<FieldP pypy.interpreter.executioncontext.ExecutionContext.inst_topframeref 136>)
p43 = force_token()
p44 = getfield_gc_r(p41, descr=<FieldP pypy.interpreter.executioncontext.ExecutionContext.inst_w_tracefunc 176 pure>)
guard_value(p44, ConstPtr(null), descr=<Guard0x10809a920>) [p0, p4, p5, p8, p13, p41, p44, p43, p42, i38, None]
i46 = getfield_gc_i(p41, descr=<FieldU pypy.interpreter.executioncontext.ExecutionContext.inst_profilefunc 112 pure>)
i47 = int_is_zero(i46)
guard_true(i47, descr=<Guard0x1080a2530>) [p0, p4, p5, p8, p13, p41, p44, p43, p42, i38, None]
enter_portal_frame(19, 4348)
debug_merge_point(1, 1, '(pypyjit: get_printable_location disabled. no debug_print)')
debug_merge_point(1, 1, '(pypyjit: get_printable_location disabled. no debug_print)')
debug_merge_point(1, 1, '(pypyjit: get_printable_location disabled. no debug_print)')
i51 = int_add_ovf(i38, 234)
guard_no_overflow(descr=<Guard0x1080a24e8>) [p0, p4, p5, p8, p13, p41, p44, p43, p42, i38, None]
debug_merge_point(1, 1, '(pypyjit: get_printable_location disabled. no debug_print)')
leave_portal_frame(19)
debug_merge_point(0, 0, '(pypyjit: get_printable_location disabled. no debug_print)')
debug_merge_point(0, 0, '(pypyjit: get_printable_location disabled. no debug_print)')
i54 = getfield_raw_i(4420303776, descr=<FieldS pypysig_long_struct.c_value 0>)
setfield_gc(ConstPtr(ptr55), i51, descr=<FieldS pypy.objspace.std.typeobject.IntMutableCell.inst_intvalue 8>)
i57 = int_lt(i54, 0)
guard_false(i57, descr=<Guard0x10809a860>) [p0, p4, p5, p8, p13, i54, None, None, None, None]
debug_merge_point(0, 0, '(pypyjit: get_printable_location disabled. no debug_print)')
label(p0, p13, p4, p5, p8, i21, i18, p41, p42, descr=TargetToken(4429777680))
debug_merge_point(0, 0, '(pypyjit: get_printable_location disabled. no debug_print)')
i58 = int_lt(i21, i18)
guard_true(i58, descr=<Guard0x10809a800>) [p0, p4, p5, p8, p13, i18, i21]
i60 = int_add(i21, 1)
debug_merge_point(0, 0, '(pypyjit: get_printable_location disabled. no debug_print)')
setfield_gc(p8, i60, descr=<FieldS pypy.module.__builtin__.functional.W_IntRangeIterator.inst_current 8>)
guard_not_invalidated(descr=<Guard0x10809a7a0>) [p0, p4, p5, p8, p13, i21]
debug_merge_point(0, 0, '(pypyjit: get_printable_location disabled. no debug_print)')
debug_merge_point(0, 0, '(pypyjit: get_printable_location disabled. no debug_print)')
setfield_gc(ConstPtr(ptr61), i21, descr=<FieldS pypy.objspace.std.typeobject.IntMutableCell.inst_intvalue 8>)
i63 = getfield_gc_i(ConstPtr(ptr62), descr=<FieldS pypy.objspace.std.typeobject.IntMutableCell.inst_intvalue 8>)
debug_merge_point(0, 0, '(pypyjit: get_printable_location disabled. no debug_print)')
p64 = force_token()
enter_portal_frame(19, 4348)
debug_merge_point(1, 1, '(pypyjit: get_printable_location disabled. no debug_print)')
debug_merge_point(1, 1, '(pypyjit: get_printable_location disabled. no debug_print)')
debug_merge_point(1, 1, '(pypyjit: get_printable_location disabled. no debug_print)')
i68 = int_add_ovf(i63, 234)
guard_no_overflow(descr=<Guard0x10809a6e0>) [p0, p4, p5, p8, p13, p41, i63, p64, p42, None]
debug_merge_point(1, 1, '(pypyjit: get_printable_location disabled. no debug_print)')
leave_portal_frame(19)
debug_merge_point(0, 0, '(pypyjit: get_printable_location disabled. no debug_print)')
debug_merge_point(0, 0, '(pypyjit: get_printable_location disabled. no debug_print)')
i71 = getfield_raw_i(4420303776, descr=<FieldS pypysig_long_struct.c_value 0>)
setfield_gc(ConstPtr(ptr72), i68, descr=<FieldS pypy.objspace.std.typeobject.IntMutableCell.inst_intvalue 8>)
i74 = int_lt(i71, 0)
guard_false(i74, descr=<Guard0x10809a680>) [p0, p4, p5, p8, p13, i71, None, None, None]
debug_merge_point(0, 0, '(pypyjit: get_printable_location disabled. no debug_print)')
jump(p0, p13, p4, p5, p8, i60, i18, p41, p42, descr=TargetToken(4429777680))
```


