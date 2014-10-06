#!/usr/bin/python3

import functools
import subprocess
import tkinter
import tkinter.filedialog as fdialog


def get_filename(root, label):
    filename = fdialog.askopenfilename(
        parent=root,
        defaultextension='.bit',
        filetypes=[('bit files', '.bit')])
    label['text'] = filename


def launch_impl(filename, image_size, is_with_source,
                frequency, is_colored, interpolation):
    # コマンドを生成
    command = ["../core//bin/core",
               "--filename=" + filename,
               "--image-size=" + image_size.get(),
               "--frequency=" + frequency.get(),
               "--interpolation=" + interpolation.get(),
               "--output-directory=img"]
    if is_colored.get() > 0:
        command.append("--colored")
    if is_with_source.get() > 0:
        command.append("--show-source")
    # コマンドを表示
    for item in command:
        print(item, end=" ")
    print("")
    # コマンドを実行
    subprocess.call(command)


def launch(frame,
           filename_label, image_size, is_with_source,
           frequency, is_colored, interpolation):
    if filename_label.cget('text') != 'none':
        filename = filename_label.cget('text')
        frame.destroy()
        launch_impl(filename, image_size, is_with_source,
                    frequency, is_colored, interpolation)


def main_impl():
    padding = 5

    # GUI
    launcher_frame = tkinter.Tk()
    launcher_frame.wm_title("launcher")

    image_size = tkinter.StringVar()
    image_size.set("middle")
    is_with_source = tkinter.IntVar()
    is_with_source.set(1)
    frequency = tkinter.StringVar()
    frequency.set("40")
    is_colored = tkinter.IntVar()
    is_colored.set(0)
    interpolation = tkinter.StringVar()
    interpolation.set("linear")

    # GUI components
    tkinter.Label(launcher_frame, text='ビットファイル名') \
           .grid(row=0, column=0, padx=padding, pady=padding, sticky=tkinter.W)
    filename_label = tkinter.Label(launcher_frame, text='none')
    filename_label.grid(row=0, column=1, columnspan=3,
                        padx=padding, pady=padding, sticky=tkinter.W)
    tkinter.Button(launcher_frame, text='ファイル選択',
                   command=functools.partial(get_filename,
                                             launcher_frame, filename_label)) \
           .grid(row=0, column=4, padx=padding, pady=padding, sticky=tkinter.W)

    tkinter.Label(launcher_frame, text='画像サイズ') \
           .grid(row=1, column=0, padx=padding, pady=padding, sticky=tkinter.W)
    tkinter.Radiobutton(text='320x240', variable=image_size, value="small") \
           .grid(row=1, column=1, padx=padding, pady=padding, sticky=tkinter.W)
    tkinter.Radiobutton(text='640x480', variable=image_size, value="middle") \
           .grid(row=1, column=2, padx=padding, pady=padding, sticky=tkinter.W)
    tkinter.Radiobutton(text='800x600', variable=image_size, value="large") \
           .grid(row=1, column=3, padx=padding, pady=padding, sticky=tkinter.W)

    tkinter.Label(launcher_frame, text='キャプチャの表示') \
           .grid(row=2, column=0, padx=padding, pady=padding, sticky=tkinter.W)
    tkinter.Radiobutton(text='なし', variable=is_with_source, value="0") \
           .grid(row=2, column=1, padx=padding, pady=padding, sticky=tkinter.W)
    tkinter.Radiobutton(text='あり', variable=is_with_source, value="1") \
           .grid(row=2, column=2, padx=padding, pady=padding, sticky=tkinter.W)

    tkinter.Label(launcher_frame, text='動作周波数') \
           .grid(row=3, column=0, padx=padding, pady=padding, sticky=tkinter.W)
    tkinter.Radiobutton(text='20MHz', variable=frequency, value="20") \
           .grid(row=3, column=1, padx=padding, pady=padding, sticky=tkinter.W)
    tkinter.Radiobutton(text='30MHz', variable=frequency, value="30") \
           .grid(row=3, column=2, padx=padding, pady=padding, sticky=tkinter.W)
    tkinter.Radiobutton(text='40MHz', variable=frequency, value="40") \
           .grid(row=3, column=3, padx=padding, pady=padding, sticky=tkinter.W)

#    tkinter.Label(launcher_frame, text='色') \
#           .grid(row=4, column=0, padx=padding, pady=padding, sticky=tkinter.W)
#    tkinter.Radiobutton(text='グレースケール', variable=is_colored, value="0") \
#           .grid(row=4, column=1, padx=padding, pady=padding, sticky=tkinter.W)
#    tkinter.Radiobutton(text='RGBA', variable=is_colored, value="1") \
#           .grid(row=4, column=2, padx=padding, pady=padding, sticky=tkinter.W)

    tkinter.Label(launcher_frame, text='補間') \
           .grid(row=4, column=0, padx=padding, pady=padding, sticky=tkinter.W)
    tkinter.Radiobutton(text='最近傍', variable=interpolation, value="nearest") \
           .grid(row=4, column=1, padx=padding, pady=padding, sticky=tkinter.W)
    tkinter.Radiobutton(text='線形', variable=interpolation, value="linear") \
           .grid(row=4, column=2, padx=padding, pady=padding, sticky=tkinter.W)

    tkinter.Button(launcher_frame, text='開始',
                   command=functools.partial(
                       launch,
                       launcher_frame, filename_label, image_size,
                       is_with_source, frequency, is_colored, interpolation)) \
           .grid(row=5, column=0, padx=padding, pady=padding, sticky=tkinter.W)

    # Main loop
    launcher_frame.mainloop()


if __name__ == '__main__':
    main_impl()
