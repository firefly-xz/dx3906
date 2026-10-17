# dx3906

STM32F103C8T6 (Blue Pill, LQFP48) 基础工程，由 STM32CubeMX 生成、Keil MDK-ARM 构建。

## 硬件 / 配置

| 项目 | 值 |
| --- | --- |
| MCU | STM32F103C8T6（`STM32F103C(8-B)Tx`） |
| 封装 | LQFP48 |
| 系统时钟 | HSI 8 MHz，未启用 PLL |
| PC13 | GPIO 推挽输出（板载 LED，低电平点亮） |
| PA9 | GPIO 外部中断，上升沿触发（`EXTI9`） |
| PA13 / PA14 | SWD 调试口（SWDIO / SWCLK） |

## 工具链

- STM32CubeMX 6.18.1（`dx3906.ioc`）
- STM32Cube FW_F1 V1.8.7
- Keil MDK-ARM V5.32（`MDK-ARM/dx3906.uvprojx`）

## 目录结构

```
Core/         CubeMX 生成的用户代码（main.c、中断向量、MSP、HAL 配置）
Drivers/      CMSIS 与 STM32F1xx HAL 驱动源码（已随工程复制）
MDK-ARM/      Keil 工程文件与启动汇编
dx3906.ioc    CubeMX 工程配置
```

## 构建

用 Keil MDK 打开 `MDK-ARM/dx3906.uvprojx` 后直接 Build，或命令行：

```sh
UV4 -b MDK-ARM/dx3906.uvprojx -o build.log
```

## 当前状态

- `main.c` 的用户代码区仍为空，主循环只把 PC13 拉低一次，尚未实现具体功能。
- PA9 的 EXTI 仅在寄存器层配置完成，NVIC 中的 `EXTI line[9:5]` 未使能，也没有 `EXTI9_5_IRQHandler`，因此该中断目前不会触发。

## 许可

`Drivers/` 下的代码版权归 STMicroelectronics 所有，遵循各自目录中的 `LICENSE.txt`；其余部分未指定许可。
