# Tips of tracing

### OSD
- How to record event
```cpp
op->osd_trace.event("enqueue op");
```

- How to record variables (OSD)
```cpp
// only integer / string
op->osd_trace.keyval("priority", op->get_req()->get_priority());
op->osd_trace.keyval("cost", op->get_req()->get_cost());
```

- Show results
```bash
cd ${CEPHPATH}/build
make ceph-osd

../src/stop.sh
LD_PRELOAD=/usr/lib/x86_64-linux-gnu/liblttng-ust-fork.so \
../src/vstart.sh --debug --new -x --localhost

ttng destroy && \
lttng create ceph && \
lttng enable-event -u zipkin:timestamp && \
lttng enable-event -u zipkin:keyval_integer && \
lttng enable-event -u zipkin:keyval_string
```