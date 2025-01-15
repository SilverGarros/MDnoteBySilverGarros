```python
with gr.Blocks(title="GPT-SoVITS WebUI") as app:
    # gr.Markdown( value=i18n( "本软件以MIT协议开源, 作者不对软件具备任何控制力, 使用软件者、传播软件导出的声音者自负全责. <br>如不认可该条款, 则不能使用或引用软件包内任何代码和文件.
    # 详见根目录<b>LICENSE</b>.") )
    with gr.Group():
        gr.Markdown(value=i18n("说话人切换"))
        with gr.Row():
            speaker_dropdown = gr.Dropdown(label=i18n("说话人名称"), choices=sorted(speaker_names, key=custom_sort_key),
                                           value=speakers_name_Default, interactive=True)
            refresh_button = gr.Button(i18n("刷新说话人"), variant="primary")
            refresh_button.click(fn=change_choices, inputs=[], outputs=[speaker_dropdown])

            speaker_dropdown.change(change_speakers_weights, [speaker_dropdown], [])

        gr.Markdown(value=i18n("具体模型切换"))
        with gr.Row():
            GPT_dropdown = gr.Dropdown(label=i18n("GPT模型列表"), choices=sorted(GPT_names, key=custom_sort_key),
                                       value=gpt_path, interactive=True)
            SoVITS_dropdown = gr.Dropdown(label=i18n("SoVITS模型列表"),
                                          choices=sorted(SoVITS_names, key=custom_sort_key), value=sovits_path,
                                          interactive=True)

            refresh_button = gr.Button(i18n("刷新模型路径"), variant="primary")

            refresh_button.click(fn=change_choices, inputs=[], outputs=[SoVITS_dropdown, GPT_dropdown])
            SoVITS_dropdown.change(change_sovits_weights, [SoVITS_dropdown], [])
            GPT_dropdown.change(change_gpt_weights, [GPT_dropdown], [])
        gr.Markdown(value=i18n("*请上传并填写参考信息"))
        with gr.Row():
            # inp_ref = gr.Audio(label=i18n("请上传3~10秒内参考音频，超过会报错！"), type="filepath")
            inp_ref = gr.Audio(label=i18n("参考音频控制在3~10秒内，否则报错！"), type="filepath",
                               default=default_audio_path)
            prompt_text = gr.Textbox(label=i18n("参考音频的文本"),
                                     default=i18n("地图上不会有感叹号标记，也没有引导玩家的路标点"),
                                     value="地图上不会有感叹号标记，也没有引导玩家的路标点")
            prompt_language = gr.Dropdown(
                label=i18n("参考音频的语种"),
                choices=[i18n("中文"), i18n("英文"), i18n("日文"), i18n("中英混合"), i18n("日英混合"),
                         i18n("多语种混合")], value=i18n("中文")
            )
        gr.Markdown(value=i18n(
            "*请填写需要合成的目标文本。中英混合选中文，日英混合选日文，中日混合暂不支持，非目标语言文本自动遗弃。"))
        with gr.Row():
            text = gr.Textbox(label=i18n("需要合成的文本"), value="")
            text_language = gr.Dropdown(
                label=i18n("需要合成的语种"),
                choices=[i18n("中文"), i18n("英文"), i18n("日文"), i18n("中英混合"), i18n("日英混合"),
                         i18n("多语种混合")], value=i18n("中文")
            )
            how_to_cut = gr.Radio(
                label=i18n("文本切分"),
                choices=[i18n("不切分"), i18n("四句切分"), i18n("50切分"), i18n("按中文句号。切分"),
                         i18n("按英文句号.切分"), i18n("按标点符号切分"), ],
                value=i18n("凑四句一切"),
                interactive=True,
            )
            with gr.Row():
                top_k = gr.Slider(minimum=1, maximum=100, step=1, label=i18n("top_k"), value=5, interactive=True)
                top_p = gr.Slider(minimum=0, maximum=1, step=0.05, label=i18n("top_p"), value=1, interactive=True)
                temperature = gr.Slider(minimum=0, maximum=1, step=0.05, label=i18n("temperature"), value=1,
                                        interactive=True)
            inference_button = gr.Button(i18n("合成语音"), variant="primary")
            output = gr.Audio(label=i18n("输出的语音"))

        inference_button.click(
            get_tts_wav,
            # [inp_ref, prompt_text, prompt_language, text, text_language, how_to_cut,top_k,top_p,temperature],
            # [output],
            [prompt_language, text, text_language, prompt_text, inp_ref, how_to_cut, top_k, top_p, temperature],
            [output],
        )

app.queue(concurrency_count=511, max_size=1022).launch(
    server_name="127.0.0.1",
    inbrowser=True,
    share=False,
    server_port=infer_ttswebui,
    debug=True
)
```