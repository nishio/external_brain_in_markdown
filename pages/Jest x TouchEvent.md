---
title: "Jest x TouchEvent"
---

ts

```typescript
  const canvas = screen.getByTestId("overlayCanvas")!;
  const touch = new Touch({
    clientX: 0,
    clientY: 0,
    identifier: 1,
    force: 0,
    altitudeAngle: 0,
    azimuthAngle: 0,
    pageX: 0,
    pageY: 0,
    radiusX: 0,
    radiusY: 0,
    rotationAngle: 0,
    screenX: 0,
    screenY: 0,
    target: canvas,
    touchType: "direct",
  });
  fireEvent(
    canvas,
    new TouchEvent("touchstart", {
      touches: [touch],
      cancelable: true,
      bubbles: true,
      targetTouches: [touch],
      changedTouches: [touch],
      shiftKey: false,
    }),
  );
```


test.tsx

```
const bindTarget = (target: Element) => {
  const defaultTouchInit: TouchInit = {
    clientX: 0,
    clientY: 0,
    identifier: 1,
    force: 0,
    altitudeAngle: 0,
    azimuthAngle: 0,
    pageX: 0,
    pageY: 0,
    radiusX: 0,
    radiusY: 0,
    rotationAngle: 0,
    screenX: 0,
    screenY: 0,
    target: target,
    touchType: "direct",
  };
  const newTouch = (opt: Partial<TouchInit>) => {
    return new Touch({ ...defaultTouchInit, ...opt });
  };
  const defaultEventInit: TouchEventInit = {
    targetTouches: [],
    touches: [],
    changedTouches: [],
    cancelable: true,
    bubbles: true,
    shiftKey: false,
  };
  const fireTouchStart = (type: string, opt: Partial<TouchEventInit>) => {
    fireEvent(target, new TouchEvent(type, { ...defaultEventInit, ...opt }));
  };
  return { newTouch, fireTouchStart };
};

test("TwoFingerGesture", async () => {
  initializeGlobalVariables();
  render(<App urlParam="blank" />);
  expect(paper.project.view.zoom).toBe(1);

  const canvas = screen.getByTestId("overlayCanvas")!;
  const { newTouch, fireTouchStart } = bindTarget(canvas);
  const t1 = newTouch({ identifier: 1, clientX: 0, clientY: 0 });
  const t2 = newTouch({ identifier: 2, clientX: 100, clientY: 100 });
  fireTouchStart("touchstart", {
    targetTouches: [t1],
    touches: [t1],
    changedTouches: [t1],
  });
  fireTouchStart("touchstart", {
    targetTouches: [t1, t2],
    touches: [t1, t2],
    changedTouches: [t2],
  });
  const t3 = newTouch({ identifier: 1, clientX: 25, clientY: 25 });
  const t4 = newTouch({ identifier: 2, clientX: 75, clientY: 75 });
  fireTouchStart("touchmove", {
    targetTouches: [t3, t4],
    touches: [t3, t4],
    changedTouches: [t3, t4],
  });

  fireTouchStart("touchend", {
    targetTouches: [t4],
    touches: [t4],
    changedTouches: [t3],
  });
  fireTouchStart("touchend", {
    targetTouches: [t3],
    touches: [],
    changedTouches: [],
  });

  expect(paper.project.view.zoom).toBe(0.5);
});
```

