# Accompanied Singing Voice Synthesis with Fully Text-controlled Melody

<!-- Google tag (gtag.js) -->
<!-- <script async src="https://www.googletagmanager.com/gtag/js?id=G-86MF0006K1"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());

  gtag('config', 'G-86MF0006K1');
</script> -->

<h2 id="abstract">Abstract</h2>

Text-to-song (TTSong) is a music generation task that synthesizes accompanied singing voices. Current TTSong methods, inherited from singing voice synthesis (SVS), require melody-related information that can sometimes be impractical, such as music scores or MIDI sequences. We present MelodyLM, the first TTSong model that generates high-quality song pieces with fully text-controlled melodies, achieving minimal user requirements and maximum control flexibility. MelodyLM explicitly models MIDI as the intermediate melody-related feature and sequentially generates vocal tracks in a language model manner, conditioned on textual and vocal prompts. The accompaniment music is subsequently synthesized by a latent diffusion model with hybrid conditioning for temporal alignment. With minimal requirements, users only need to input lyrics and a reference voice to synthesize a song sample. For full control, just input textual prompts or even directly input MIDI. Experimental results indicate that MelodyLM achieves superior performance in terms of both objective and subjective metrics. 

**Table of Contents**

1. [Abstract](#abstract)
2. [Overview of Demonstration](#overview)
3. [Target Singing Vocals + Accompaniment Prompts -> Song](#gtvocal_accompprompts_to_song)
4. [Lyrics + Target MIDI + Reference Vocals + Accompaniment Prompts -> Song](#lyrics_gtmidi_refvocal_accompprompts_to_song)
5. [Lyrics + Melody Prompts + Reference Vocals + Accompaniment Prompts -> Song](#lyrics_melodyprompts_refvocal_accompprompts_to_song)
6. [Lyrics + Melody Prompts -> Song](#lyrics_melodyprompts_to_song)
7. [Lyrics -> Song](#lyrics_to_song)

<h2 id="overview">Overview of Demonstration</h2>

We demonstrate the minimal user requirements and maximum control flexibility by gradually decreasing the degree of control. We first demonstrate the model capability by providing fully control, i.e., input singing vocals and prompts about accompaniment. Then, we gradually lower the user requirements and see how the model reacts. It is worth mentioning that the lyrics listed below are all generated using WhisperX, which could be different from the real lyrics. 

<h2 id="gtvocal_accompprompts_to_song">Target Singing Vocals + Accompaniment Prompts -> Song</h2>

We provide target singing vocals and the prompts about accompaniment to generate accompaniment music. In this scenario, the model degenerates into a accompaniment generation model. 


* Lyrics: 颜色太惆怅 学生你别慌张十里愁几多愁不如靠在我身上
   
   Pinyin: yan se tai chou chang xue sheng ni bie huang zhang shi li chou ji duo chou bu ru kao zai wo shen shang

    <table style='width: 100%;'>
        <thead>
        <tr>
            <th></th>
            <th>GT Song</th>
            <th>GT Vocal</th>
            <th>GT Accompaniment</th>
            <th>Accomp. Prompts</th>
            <th>Generated Accomp.</th>
            <th>Generated Song</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <th scope="row">wav</th>
            <td><audio controls="" ><source src="resources/samples/gtvocal_to_song/gt_song/颜色太惆怅 学生你别慌张十里愁 几多愁 不如靠在我身上.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/gtvocal_to_song/gt_vocal/颜色太惆怅 学生你别慌张十里愁 几多愁 不如靠在我身上.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/gtvocal_to_song/gt_accomp/颜色太惆怅 学生你别慌张十里愁 几多愁 不如靠在我身上.wav" type="audio/wav"></audio></td>
            <td style="text-align: center">This is a pop music piece. There is a female vocalist singing melodically in the lead. The main melody is being played by the keyboard with the bass guitar playing in the background. The rhythm is provided by an electronic drum beat. The atmosphere is easygoing. This piece could be used in the soundtrack of a sit-com movie or a TV show. </td>
            <td><audio controls="" ><source src="resources/samples/gtvocal_to_song/pred_cond_accomp/颜色太惆怅 学生你别慌张十里愁 几多愁 不如靠在我身上.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/gtvocal_to_song/pred_cond_song/颜色太惆怅 学生你别慌张十里愁 几多愁 不如靠在我身上.wav" type="audio/wav"></audio></td>
        </tr>
        </tbody>
    </table>

* Lyrics: 开启梦的多重宇宙一场完美的出走让你陪我仰望山腰
   
  Pinyin: kai qi meng de duo chong yu zhou yi chang wan mei de chu zou rang ni pei wo yang wang shan yao

    <table style='width: 100%;'>
        <thead>
        <tr>
            <th></th>
            <th>GT Song</th>
            <th>GT Vocal</th>
            <th>GT Accompaniment</th>
            <th>Accomp. Prompts</th>
            <th>Generated Accomp.</th>
            <th>Generated Song</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <th scope="row">wav</th>
            <td><audio controls="" ><source src="resources/samples/gtvocal_to_song/gt_song/开启梦的多重宇宙一场完美的出走让你陪我仰望山腰.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/gtvocal_to_song/gt_vocal/开启梦的多重宇宙一场完美的出走让你陪我仰望山腰.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/gtvocal_to_song/gt_accomp/开启梦的多重宇宙一场完美的出走让你陪我仰望山腰.wav" type="audio/wav"></audio></td>
            <td style="text-align: center">This musical recording features a pop song that consists of a passionate male vocal singing over punchy kick and snare hits, shimmering hi hats, wide electric guitar melody, distorted bass and mellow synth pad chords. It sounds energetic and addictive. </td>
            <td><audio controls="" ><source src="resources/samples/gtvocal_to_song/pred_cond_accomp/开启梦的多重宇宙一场完美的出走让你陪我仰望山腰.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/gtvocal_to_song/pred_cond_song/开启梦的多重宇宙一场完美的出走让你陪我仰望山腰.wav" type="audio/wav"></audio></td>
        </tr>
        </tbody>
    </table>

* Lyrics: 害怕什么都失去只是想要有人听听到我的不适应
   
  Pinyin: hai pa shen me dou shi qu zhi shi xiang yao you ren ting ting dao wo de bu shi ying

    <table style='width: 100%;'>
        <thead>
        <tr>
            <th></th>
            <th>GT Song</th>
            <th>GT Vocal</th>
            <th>GT Accompaniment</th>
            <th>Accomp. Prompts</th>
            <th>Generated Accomp.</th>
            <th>Generated Song</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <th scope="row">wav</th>
            <td><audio controls="" ><source src="resources/samples/gtvocal_to_song/gt_song/害怕什么都失去只是想要有人听听到我的不适应.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/gtvocal_to_song/gt_vocal/害怕什么都失去只是想要有人听听到我的不适应.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/gtvocal_to_song/gt_accomp/害怕什么都失去只是想要有人听听到我的不适应.wav" type="audio/wav"></audio></td>
            <td style="text-align: center">This is a pop music piece. There is a male vocalist singing melodically in the lead. The main tune is being played by the acoustic guitar and the electric guitar. The bass guitar is playing in the background. The rhythm is provided by a slow tempo acoustic drum beat. The atmosphere is emotional. This piece could be used in the soundtrack of a romance movie or a TV series. </td>
            <td><audio controls="" ><source src="resources/samples/gtvocal_to_song/pred_cond_accomp/害怕什么都失去只是想要有人听听到我的不适应.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/gtvocal_to_song/pred_cond_song/害怕什么都失去只是想要有人听听到我的不适应.wav" type="audio/wav"></audio></td>
        </tr>
        </tbody>
    </table>

<!-- * Lyrics: 每当要掀开我接受你的挑战放大你给的爱填满我的心坎
   
  Pinyin: mei dao yao xian kai wo jie shou ni de tiao zhan fang da ni gei wo de ai tian man wo de xin kan

    <table style='width: 100%;'>
        <thead>
        <tr>
            <th></th>
            <th>GT Song</th>
            <th>GT Vocal</th>
            <th>GT Accompaniment</th>
            <th>Accomp. Prompts</th>
            <th>Generated Accomp.</th>
            <th>Generated Song</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <th scope="row">wav</th>
            <td><audio controls="" ><source src="resources/samples/gtvocal_to_song/gt_song/每当要掀开我接受你的挑战放大你给的爱填满我的心坎.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/gtvocal_to_song/gt_vocal/每当要掀开我接受你的挑战放大你给的爱填满我的心坎.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/gtvocal_to_song/gt_accomp/每当要掀开我接受你的挑战放大你给的爱填满我的心坎.wav" type="audio/wav"></audio></td>
            <td style="text-align: center">This is a house music piece. There is a female vocalist singing melodically in the lead. The melody is being played by the synth bass while the rhythm is provided by an electronic drum beat. The atmosphere is danceable and energetic. This piece could be played at nightclubs and dance clubs. </td>
            <td><audio controls="" ><source src="resources/samples/gtvocal_to_song/pred_cond_accomp/每当要掀开我接受你的挑战放大你给的爱填满我的心坎.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/gtvocal_to_song/pred_cond_song/每当要掀开我接受你的挑战放大你给的爱填满我的心坎.wav" type="audio/wav"></audio></td>
        </tr>
        </tbody>
    </table> -->

* Lyrics: 你给我的爱如花盛开如花落败日渐苍白你转身离开留下空白
   
  Pinyin: ni gei wo de ai ru hua sheng kai ru hua luo bai ri jian cang bai ni zhuan shen li kai liu xia kong bai

    <table style='width: 100%;'>
        <thead>
        <tr>
            <th></th>
            <th>GT Song</th>
            <th>GT Vocal</th>
            <th>GT Accompaniment</th>
            <th>Accomp. Prompts</th>
            <th>Generated Accomp.</th>
            <th>Generated Song</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <th scope="row">wav</th>
            <td><audio controls="" ><source src="resources/samples/gtvocal_to_song/gt_song/你给我的爱如花盛开如花落败日渐苍白你转身离开留下空白.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/gtvocal_to_song/gt_vocal/你给我的爱如花盛开如花落败日渐苍白你转身离开留下空白.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/gtvocal_to_song/gt_accomp/你给我的爱如花盛开如花落败日渐苍白你转身离开留下空白.wav" type="audio/wav"></audio></td>
            <td style="text-align: center">This musical recording features a flat female vocal singing over sustained strings melody and mellow piano melody. It sounds emotional, passionate and the recording is noisy and in mono. </td>
            <td><audio controls="" ><source src="resources/samples/gtvocal_to_song/pred_cond_accomp/你给我的爱如花盛开如花落败日渐苍白你转身离开留下空白.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/gtvocal_to_song/pred_cond_song/你给我的爱如花盛开如花落败日渐苍白你转身离开留下空白.wav" type="audio/wav"></audio></td>
        </tr>
        </tbody>
    </table>

* Lyrics: 你脸上的唇印暧昧得很仔细甜得像茉莉花开的香气
   
  Pinyin: ni lian shang de chun yin ai mei de hen zi xi tian de xiang mo li hua kai de xiang qi

    <table style='width: 100%;'>
        <thead>
        <tr>
            <th></th>
            <th>GT Song</th>
            <th>GT Vocal</th>
            <th>GT Accompaniment</th>
            <th>Accomp. Prompts</th>
            <th>Generated Accomp.</th>
            <th>Generated Song</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <th scope="row">wav</th>
            <td><audio controls="" ><source src="resources/samples/gtvocal_to_song/gt_song/你脸上的唇印 暧昧得很仔细甜得像茉莉花开的香气.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/gtvocal_to_song/gt_vocal/你脸上的唇印 暧昧得很仔细甜得像茉莉花开的香气.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/gtvocal_to_song/gt_accomp/你脸上的唇印 暧昧得很仔细甜得像茉莉花开的香气.wav" type="audio/wav"></audio></td>
            <td style="text-align: center">This is a teen pop music piece. There is a female vocalist singing melodically. The main tune is being played by the acoustic guitar and the electric guitar while the bass guitar is playing in the background. The rhythm is provided by an electronic drum beat. The atmosphere is easygoing. This piece could be used in the soundtrack of a teenage drama TV show. </td>
            <td><audio controls="" ><source src="resources/samples/gtvocal_to_song/pred_cond_accomp/你脸上的唇印 暧昧得很仔细甜得像茉莉花开的香气.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/gtvocal_to_song/pred_cond_song/你脸上的唇印 暧昧得很仔细甜得像茉莉花开的香气.wav" type="audio/wav"></audio></td>
        </tr>
        </tbody>
    </table>

* Lyrics: 其实对我来说不算惊讶我可以歇斯底里避免了尴尬
   
  Pinyin: qi shi dui wo lai shuo bu suan jing ya wo ke yi xie si di li bi mian le gan ga

    <table style='width: 100%;'>
        <thead>
        <tr>
            <th></th>
            <th>GT Song</th>
            <th>GT Vocal</th>
            <th>GT Accompaniment</th>
            <th>Accomp. Prompts</th>
            <th>Generated Accomp.</th>
            <th>Generated Song</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <th scope="row">wav</th>
            <td><audio controls="" ><source src="resources/samples/gtvocal_to_song/gt_song/其实对我来说不算惊讶我可以歇斯底里避免了尴尬.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/gtvocal_to_song/gt_vocal/其实对我来说不算惊讶我可以歇斯底里避免了尴尬.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/gtvocal_to_song/gt_accomp/其实对我来说不算惊讶我可以歇斯底里避免了尴尬.wav" type="audio/wav"></audio></td>
            <td style="text-align: center">The recorded music features a pop song that consists of harmonizing male vocals singing over mellow piano chords. It sounds passionate and emotional, even though the recording is noisy and in mono. </td>
            <td><audio controls="" ><source src="resources/samples/gtvocal_to_song/pred_cond_accomp/其实对我来说不算惊讶我可以歇斯底里避免了尴尬.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/gtvocal_to_song/pred_cond_song/其实对我来说不算惊讶我可以歇斯底里避免了尴尬.wav" type="audio/wav"></audio></td>
        </tr>
        </tbody>
    </table>

<!-- * Lyrics: 我们的故事终于就这样结了尾你不再是是我的谁
   
  Pinyin: wo men de gu shi zhong yu jiu zhe yang jie le wei ni bu zai shi shi wo de shei

    <table style='width: 100%;'>
        <thead>
        <tr>
            <th></th>
            <th>GT Song</th>
            <th>GT Vocal</th>
            <th>GT Accompaniment</th>
            <th>Accomp. Prompts</th>
            <th>Generated Accomp.</th>
            <th>Generated Song</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <th scope="row">wav</th>
            <td><audio controls="" ><source src="resources/samples/gtvocal_to_song/gt_song/我们的故事终于就这样结了尾你不再是 是我的谁.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/gtvocal_to_song/gt_vocal/我们的故事终于就这样结了尾你不再是 是我的谁.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/gtvocal_to_song/gt_accomp/我们的故事终于就这样结了尾你不再是 是我的谁.wav" type="audio/wav"></audio></td>
            <td style="text-align: center">This is a pop music piece. There is a female vocalist singing melodically in the lead. The melody is being played by the acoustic guitar and the electric guitar while the bass guitar is playing in the background. The rhythm is provided by a slow tempo acoustic drum beat. The atmosphere is emotional. This piece could be used in the soundtrack of a romance/drama movie, especially during the scenes where the characters are missing each other. </td>
            <td><audio controls="" ><source src="resources/samples/gtvocal_to_song/pred_cond_accomp/我们的故事终于就这样结了尾你不再是 是我的谁.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/gtvocal_to_song/pred_cond_song/我们的故事终于就这样结了尾你不再是 是我的谁.wav" type="audio/wav"></audio></td>
        </tr>
        </tbody>
    </table> -->


* Lyrics: 只有我懂你晚安的意义是想你的讯号
   
  Pinyin: zhi you wo dong ni wan an de yi yi shi xiang ni de xun hao

    <table style='width: 100%;'>
        <thead>
        <tr>
            <th></th>
            <th>GT Song</th>
            <th>GT Vocal</th>
            <th>GT Accompaniment</th>
            <th>Accomp. Prompts</th>
            <th>Generated Accomp.</th>
            <th>Generated Song</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <th scope="row">wav</th>
            <td><audio controls="" ><source src="resources/samples/gtvocal_to_song/gt_song/只有我懂你晚安的意义是想你的讯号.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/gtvocal_to_song/gt_vocal/只有我懂你晚安的意义是想你的讯号.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/gtvocal_to_song/gt_accomp/只有我懂你晚安的意义是想你的讯号.wav" type="audio/wav"></audio></td>
            <td style="text-align: center">A male singer sings this cool hip hop melody with backup singers in vocal harmony. The song is medium tempo with a piano accompaniment, percussive bass line, steady drumming rhythm, clapping percussions, and keyboard accompaniment. The clip is emotional and romantic with a cool dance groove. </td>
            <td><audio controls="" ><source src="resources/samples/gtvocal_to_song/pred_cond_accomp/只有我懂你晚安的意义是想你的讯号.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/gtvocal_to_song/pred_cond_song/只有我懂你晚安的意义是想你的讯号.wav" type="audio/wav"></audio></td>
        </tr>
        </tbody>
    </table>


<h2 id="lyrics_gtmidi_refvocal_accompprompts_to_song">Lyrics + Target MIDI + Reference Vocals + Accompaniment Prompts -> Song</h2>

We drop the target vocal input and provide lyrics, target MIDI sequences, and vocal references to generate target vocals, along with the accompaniments. The target MIDI sequences (GT MIDI) are extracted using ROSVOT, which could leave some errors. 

* Lyrics: 当记忆的线缠绕过往支离破碎

  Pinyin: dang ji yi de xian chan rao guo wang zhi li po sui

    <table style='width: 100%;'>
        <thead>
        <tr>
            <th></th>
            <th>GT Song</th>
            <th>GT Vocal</th>
            <th>GT MIDI</th>
            <th>Accomp. Prompts</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <th scope="row">wav</th>
            <td><audio controls="" ><source src="resources/samples/lyrics_gtmidi_vocalref_to_song/gt_song/当记忆的线缠绕过往支离破碎.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_gtmidi_vocalref_to_song/gt_vocal/当记忆的线缠绕过往支离破碎.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_gtmidi_vocalref_to_song/gt_midi/当记忆的线缠绕过往支离破碎.wav" type="audio/wav"></audio></td>
            <td style="text-align: center">The recording features a song that consists of a flat female vocal singing over shimmering hi hats, punchy kick and groovy bass. The recording is noisy and in mono, as it was probably recorded with a phone. </td>
        </tr>
        </tbody>
    </table>

    <table style='width: 100%;'>
        <thead>
        <tr>
            <th></th>
            <th>Ref. Vocal</th>
            <th>Generated Vocal</th>
            <th>Generated Accomp.</th>
            <th>Generated Song</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <th scope="row">wav</th>
            <td><audio controls="" ><source src="resources/samples/lyrics_gtmidi_vocalref_to_song/ref_vocal/当记忆的线缠绕过往支离破碎.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_gtmidi_vocalref_to_song/pred_vocal/当记忆的线缠绕过往支离破碎.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_gtmidi_vocalref_to_song/pred_cond_accomp/当记忆的线缠绕过往支离破碎.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_gtmidi_vocalref_to_song/pred_cond_song/当记忆的线缠绕过往支离破碎.wav" type="audio/wav"></audio></td>
        </tr>
        </tbody>
    </table>

* Lyrics: 完美无缺幸福兜了一个圈那些美好的兜圈

  Pinyin: wan mei wu que xing fu dou le yi ge quan na xie mei hao de dou quan

    <table style='width: 100%;'>
        <thead>
        <tr>
            <th></th>
            <th>GT Song</th>
            <th>GT Vocal</th>
            <th>GT MIDI</th>
            <th>Accomp. Prompts</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <th scope="row">wav</th>
            <td><audio controls="" ><source src="resources/samples/lyrics_gtmidi_vocalref_to_song/gt_song/完美无缺幸福兜了一个圈那些美好的兜圈.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_gtmidi_vocalref_to_song/gt_vocal/完美无缺幸福兜了一个圈那些美好的兜圈.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_gtmidi_vocalref_to_song/gt_midi/完美无缺幸福兜了一个圈那些美好的兜圈.wav" type="audio/wav"></audio></td>
            <td style="text-align: center">This slow pop song features a male voice singing the main melody. This is accompanied by percussion playing a simple beat. The bass plays the root notes of the chords. A guitar plays chords in the background. The mood of this song is romantic. There are no other instruments in this song. This song can be played in a romantic movie. </td>
        </tr>
        </tbody>
    </table>

    <table style='width: 100%;'>
        <thead>
        <tr>
            <th></th>
            <th>Ref. Vocal</th>
            <th>Generated Vocal</th>
            <th>Generated Accomp.</th>
            <th>Generated Song</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <th scope="row">wav</th>
            <td><audio controls="" ><source src="resources/samples/lyrics_gtmidi_vocalref_to_song/ref_vocal/完美无缺幸福兜了一个圈那些美好的兜圈.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_gtmidi_vocalref_to_song/pred_vocal/完美无缺幸福兜了一个圈那些美好的兜圈.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_gtmidi_vocalref_to_song/pred_cond_accomp/完美无缺幸福兜了一个圈那些美好的兜圈.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_gtmidi_vocalref_to_song/pred_cond_song/完美无缺幸福兜了一个圈那些美好的兜圈.wav" type="audio/wav"></audio></td>
        </tr>
        </tbody>
    </table>

* Lyrics: 千万记得天涯有人在等待

  Pinyin: qian wan ji de tian ya you ren zai deng dai

    <table style='width: 100%;'>
        <thead>
        <tr>
            <th></th>
            <th>GT Song</th>
            <th>GT Vocal</th>
            <th>GT MIDI</th>
            <th>Accomp. Prompts</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <th scope="row">wav</th>
            <td><audio controls="" ><source src="resources/samples/lyrics_gtmidi_vocalref_to_song/gt_song/千万记得天涯有人在等待.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_gtmidi_vocalref_to_song/gt_vocal/千万记得天涯有人在等待.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_gtmidi_vocalref_to_song/gt_midi/千万记得天涯有人在等待.wav" type="audio/wav"></audio></td>
            <td style="text-align: center">This recording demonstrates a cover of a pop song and it consists of a passionate female vocal singing over sustained strings melody and mellow piano chords. It sounds emotional, passionate and the recording is noisy and in mono. </td>
        </tr>
        </tbody>
    </table>

    <table style='width: 100%;'>
        <thead>
        <tr>
            <th></th>
            <th>Ref. Vocal</th>
            <th>Generated Vocal</th>
            <th>Generated Accomp.</th>
            <th>Generated Song</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <th scope="row">wav</th>
            <td><audio controls="" ><source src="resources/samples/lyrics_gtmidi_vocalref_to_song/ref_vocal/千万记得天涯有人在等待.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_gtmidi_vocalref_to_song/pred_vocal/千万记得天涯有人在等待.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_gtmidi_vocalref_to_song/pred_cond_accomp/千万记得天涯有人在等待.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_gtmidi_vocalref_to_song/pred_cond_song/千万记得天涯有人在等待.wav" type="audio/wav"></audio></td>
        </tr>
        </tbody>
    </table>

* Lyrics: 只想余生有个伴苦了酸甜一起分担

  Pinyin: zhi xiang yu sheng you ge ban ku le suan tian yi qi fen dan

    <table style='width: 100%;'>
        <thead>
        <tr>
            <th></th>
            <th>GT Song</th>
            <th>GT Vocal</th>
            <th>GT MIDI</th>
            <th>Accomp. Prompts</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <th scope="row">wav</th>
            <td><audio controls="" ><source src="resources/samples/lyrics_gtmidi_vocalref_to_song/gt_song/只想余生有个伴苦了酸甜一起分担.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_gtmidi_vocalref_to_song/gt_vocal/只想余生有个伴苦了酸甜一起分担.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_gtmidi_vocalref_to_song/gt_midi/只想余生有个伴苦了酸甜一起分担.wav" type="audio/wav"></audio></td>
            <td style="text-align: center">This slow pop song features a male voice singing the main melody. The voice is emotional. This is accompanied by a bass playing the root notes of the chords. After one line, a synth swell is played. A piano plays chords in the background. The mood of this song is romantic. This song can be played in a romantic movie. </td>
        </tr>
        </tbody>
    </table>

    <table style='width: 100%;'>
        <thead>
        <tr>
            <th></th>
            <th>Ref. Vocal</th>
            <th>Generated Vocal</th>
            <th>Generated Accomp.</th>
            <th>Generated Song</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <th scope="row">wav</th>
            <td><audio controls="" ><source src="resources/samples/lyrics_gtmidi_vocalref_to_song/ref_vocal/只想余生有个伴苦了酸甜一起分担.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_gtmidi_vocalref_to_song/pred_vocal/只想余生有个伴苦了酸甜一起分担.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_gtmidi_vocalref_to_song/pred_cond_accomp/只想余生有个伴苦了酸甜一起分担.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_gtmidi_vocalref_to_song/pred_cond_song/只想余生有个伴苦了酸甜一起分担.wav" type="audio/wav"></audio></td>
        </tr>
        </tbody>
    </table>

* Lyrics: 拼尽全力挣扎只为能成为不同人啊你好累对吗

  Pinyin: pin jin quan li zheng zha zhi wei neng cheng wei bu tong ren a ni hao lei dui ma

    <table style='width: 100%;'>
        <thead>
        <tr>
            <th></th>
            <th>GT Song</th>
            <th>GT Vocal</th>
            <th>GT MIDI</th>
            <th>Accomp. Prompts</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <th scope="row">wav</th>
            <td><audio controls="" ><source src="resources/samples/lyrics_gtmidi_vocalref_to_song/gt_song/拼尽全力挣扎只为能成为不同人啊你好累对吗.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_gtmidi_vocalref_to_song/gt_vocal/拼尽全力挣扎只为能成为不同人啊你好累对吗.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_gtmidi_vocalref_to_song/gt_midi/拼尽全力挣扎只为能成为不同人啊你好累对吗.wav" type="audio/wav"></audio></td>
            <td style="text-align: center">There is a male vocalist singing melodically. The main tune is being played by the acoustic guitar and the electric guitar while the bass guitar is playing in the background. The rhythm is provided by a simple acoustic drum beat. The atmosphere is religious. </td>
        </tr>
        </tbody>
    </table>

    <table style='width: 100%;'>
        <thead>
        <tr>
            <th></th>
            <th>Ref. Vocal</th>
            <th>Generated Vocal</th>
            <th>Generated Accomp.</th>
            <th>Generated Song</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <th scope="row">wav</th>
            <td><audio controls="" ><source src="resources/samples/lyrics_gtmidi_vocalref_to_song/ref_vocal/拼尽全力挣扎只为能成为不同人啊你好累对吗.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_gtmidi_vocalref_to_song/pred_vocal/拼尽全力挣扎只为能成为不同人啊你好累对吗.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_gtmidi_vocalref_to_song/pred_cond_accomp/拼尽全力挣扎只为能成为不同人啊你好累对吗.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_gtmidi_vocalref_to_song/pred_cond_song/拼尽全力挣扎只为能成为不同人啊你好累对吗.wav" type="audio/wav"></audio></td>
        </tr>
        </tbody>
    </table>

* Lyrics: 汽笛声回荡在空气落雨的痕迹被遗忘代替

  Pinyin: qi di sheng hui dang zai kong qi luo yu de heng ji bei yi wang dai ti

    <table style='width: 100%;'>
        <thead>
        <tr>
            <th></th>
            <th>GT Song</th>
            <th>GT Vocal</th>
            <th>GT MIDI</th>
            <th>Accomp. Prompts</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <th scope="row">wav</th>
            <td><audio controls="" ><source src="resources/samples/lyrics_gtmidi_vocalref_to_song/gt_song/汽笛声回荡在空气落雨的痕迹被遗忘代替.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_gtmidi_vocalref_to_song/gt_vocal/汽笛声回荡在空气落雨的痕迹被遗忘代替.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_gtmidi_vocalref_to_song/gt_midi/汽笛声回荡在空气落雨的痕迹被遗忘代替.wav" type="audio/wav"></audio></td>
            <td style="text-align: center">A female vocalist sings this melancholic melody. The tempo is slow with a romantic piano accompaniment. The song is soft, mellow, poignant, emotional,sentimental, romantic, melancholic, sad, lonely,and wistful. This song is a Pop. </td>
        </tr>
        </tbody>
    </table>

    <table style='width: 100%;'>
        <thead>
        <tr>
            <th></th>
            <th>Ref. Vocal</th>
            <th>Generated Vocal</th>
            <th>Generated Accomp.</th>
            <th>Generated Song</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <th scope="row">wav</th>
            <td><audio controls="" ><source src="resources/samples/lyrics_gtmidi_vocalref_to_song/ref_vocal/汽笛声回荡在空气落雨的痕迹被遗忘代替.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_gtmidi_vocalref_to_song/pred_vocal/汽笛声回荡在空气落雨的痕迹被遗忘代替.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_gtmidi_vocalref_to_song/pred_cond_accomp/汽笛声回荡在空气落雨的痕迹被遗忘代替.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_gtmidi_vocalref_to_song/pred_cond_song/汽笛声回荡在空气落雨的痕迹被遗忘代替.wav" type="audio/wav"></audio></td>
        </tr>
        </tbody>
    </table>



* Lyrics: 我们并肩走过许多地方你的出现也曾像夜的极光

  Pinyin: wo men bing jian zou guo xu duo di fang ni de chu xian ye ceng xiang ye de ji guang

    <table style='width: 100%;'>
        <thead>
        <tr>
            <th></th>
            <th>GT Song</th>
            <th>GT Vocal</th>
            <th>GT MIDI</th>
            <th>Accomp. Prompts</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <th scope="row">wav</th>
            <td><audio controls="" ><source src="resources/samples/lyrics_gtmidi_vocalref_to_song/gt_song/我们并肩走过许多地方你的出现也曾像夜的极光.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_gtmidi_vocalref_to_song/gt_vocal/我们并肩走过许多地方你的出现也曾像夜的极光.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_gtmidi_vocalref_to_song/gt_midi/我们并肩走过许多地方你的出现也曾像夜的极光.wav" type="audio/wav"></audio></td>
            <td style="text-align: center">This is a techno/house music piece. There is a female vocalist singing melodically in the lead. The melody is being played by a piano while the bass guitar is playing in the background. The rhythm is provided by a slow tempo acoustic drum beat. The atmosphere is mellow. This piece can be used in the soundtrack of a teenage drama TV series as the opening theme. </td>
        </tr>
        </tbody>
    </table>

    <table style='width: 100%;'>
        <thead>
        <tr>
            <th></th>
            <th>Ref. Vocal</th>
            <th>Generated Vocal</th>
            <th>Generated Accomp.</th>
            <th>Generated Song</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <th scope="row">wav</th>
            <td><audio controls="" ><source src="resources/samples/lyrics_gtmidi_vocalref_to_song/ref_vocal/我们并肩走过许多地方你的出现也曾像夜的极光.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_gtmidi_vocalref_to_song/pred_vocal/我们并肩走过许多地方你的出现也曾像夜的极光.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_gtmidi_vocalref_to_song/pred_cond_accomp/我们并肩走过许多地方你的出现也曾像夜的极光.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_gtmidi_vocalref_to_song/pred_cond_song/我们并肩走过许多地方你的出现也曾像夜的极光.wav" type="audio/wav"></audio></td>
        </tr>
        </tbody>
    </table>
    
* Lyrics: 盛开在夏天

  Pinyin: sheng kai zai xia tian

    <table style='width: 100%;'>
        <thead>
        <tr>
            <th></th>
            <th>GT Song</th>
            <th>GT Vocal</th>
            <th>GT MIDI</th>
            <th>Accomp. Prompts</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <th scope="row">wav</th>
            <td><audio controls="" ><source src="resources/samples/lyrics_gtmidi_vocalref_to_song/gt_song/盛开在夏天.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_gtmidi_vocalref_to_song/gt_vocal/盛开在夏天.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_gtmidi_vocalref_to_song/gt_midi/盛开在夏天.wav" type="audio/wav"></audio></td>
            <td style="text-align: center">This is a pop music piece. There is a male vocalist singing melodically in the lead. The main melody is being played by the acoustic guitar and the electric guitar while the bass guitar is playing in the background. The rhythm is provided by a simple acoustic drum beat. The atmosphere is easygoing. This piece could be used in the soundtrack of a teenage drama TV series as the opening theme. </td>
        </tr>
        </tbody>
    </table>

    <table style='width: 100%;'>
        <thead>
        <tr>
            <th></th>
            <th>Ref. Vocal</th>
            <th>Generated Vocal</th>
            <th>Generated Accomp.</th>
            <th>Generated Song</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <th scope="row">wav</th>
            <td><audio controls="" ><source src="resources/samples/lyrics_gtmidi_vocalref_to_song/ref_vocal/盛开在夏天.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_gtmidi_vocalref_to_song/pred_vocal/盛开在夏天.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_gtmidi_vocalref_to_song/pred_cond_accomp/盛开在夏天.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_gtmidi_vocalref_to_song/pred_cond_song/盛开在夏天.wav" type="audio/wav"></audio></td>
        </tr>
        </tbody>
    </table>

* Lyrics: 好像现在的我

  Pinyin: hao xiang xian zai de wo

    <table style='width: 100%;'>
        <thead>
        <tr>
            <th></th>
            <th>GT Song</th>
            <th>GT Vocal</th>
            <th>GT MIDI</th>
            <th>Accomp. Prompts</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <th scope="row">wav</th>
            <td><audio controls="" ><source src="resources/samples/lyrics_gtmidi_vocalref_to_song/gt_song/好像现在的我.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_gtmidi_vocalref_to_song/gt_vocal/好像现在的我.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_gtmidi_vocalref_to_song/gt_midi/好像现在的我.wav" type="audio/wav"></audio></td>
            <td style="text-align: center">The recorded music features a hip hop song that consists of a flat male vocal singing over punchy kick and snare hits, shimmering hi hats and groovy bass. </td>
        </tr>
        </tbody>
    </table>

    <table style='width: 100%;'>
        <thead>
        <tr>
            <th></th>
            <th>Ref. Vocal</th>
            <th>Generated Vocal</th>
            <th>Generated Accomp.</th>
            <th>Generated Song</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <th scope="row">wav</th>
            <td><audio controls="" ><source src="resources/samples/lyrics_gtmidi_vocalref_to_song/ref_vocal/好像现在的我.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_gtmidi_vocalref_to_song/pred_vocal/好像现在的我.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_gtmidi_vocalref_to_song/pred_cond_accomp/好像现在的我.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_gtmidi_vocalref_to_song/pred_cond_song/好像现在的我.wav" type="audio/wav"></audio></td>
        </tr>
        </tbody>
    </table>


<h2 id="lyrics_melodyprompts_refvocal_accompprompts_to_song">Lyrics + Melody Prompts + Reference Vocals + Accompaniment Prompts -> Song</h2>

We drop the target MIDI sequences, and replace them with the melody prompts to generate the desired melodies.

* Lyrics: 你奔跑的方向是没我的地方

  Pinyin: ni ben pao de fang xiang shi mei wo de di fang

    <table style='width: 100%;'>
        <thead>
        <tr>
            <th></th>
            <th>GT Song</th>
            <th>GT Vocal</th>
            <th>GT MIDI</th>
            <th>Melody Prompts</th>
            <th>Accomp. Prompts</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <th scope="row">wav</th>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/gt_song/你奔跑的方向是没我的地方.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/gt_vocal/你奔跑的方向是没我的地方.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/gt_midi/你奔跑的方向是没我的地方.wav" type="audio/wav"></audio></td>
            <td style="text-align: center">This melody, anchored in G major, progresses at a high pitch and slow tempo over a medium period of time, draped in upbeat and lively aura.</td>
            <td style="text-align: center">The recorded music showcases a song that consists of a passionate female vocal, alongside wide harmonizing vocals, singing over wooden percussion, shimmering bells melody and groovy bass. It sounds happy, fun and joyful. </td>
        </tr>
        </tbody>
    </table>

    <table style='width: 100%;'>
        <thead>
        <tr>
            <th></th>
            <th>Ref. Vocal</th>
            <th>Generated MIDI</th>
            <th>Generated Vocal</th>
            <th>Generated Accomp.</th>
            <th>Generated Song</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <th scope="row">wav</th>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/ref_vocal/你奔跑的方向是没我的地方.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/pred_midi/你奔跑的方向是没我的地方.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/pred_vocal/你奔跑的方向是没我的地方.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/pred_cond_accomp/你奔跑的方向是没我的地方.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/pred_cond_song/你奔跑的方向是没我的地方.wav" type="audio/wav"></audio></td>
        </tr>
        </tbody>
    </table>

* Lyrics: 只想有你在身边 Yeah

  Pinyin: zhi xiang you ni zai shen bian yeah

    <table style='width: 100%;'>
        <thead>
        <tr>
            <th></th>
            <th>GT Song</th>
            <th>GT Vocal</th>
            <th>GT MIDI</th>
            <th>Melody Prompts</th>
            <th>Accomp. Prompts</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <th scope="row">wav</th>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/gt_song/只想有你在身边 Yeah.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/gt_vocal/只想有你在身边 Yeah.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/gt_midi/只想有你在身边 Yeah.wav" type="audio/wav"></audio></td>
            <td style="text-align: center">Featuring a melody in C sharp minor with a relatively high pitch and low tempo over a short period, the song segment carries a easygoing tone.</td>
            <td style="text-align: center">This musical recording features a pop song that consists of a passionate female vocal singing over punchy kick, shimmering hi hats, mellow synth bass and simple synth lead melody. It sounds emotional, passionate and heartfelt. </td>
        </tr>
        </tbody>
    </table>

    <table style='width: 100%;'>
        <thead>
        <tr>
            <th></th>
            <th>Ref. Vocal</th>
            <th>Generated MIDI</th>
            <th>Generated Vocal</th>
            <th>Generated Accomp.</th>
            <th>Generated Song</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <th scope="row">wav</th>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/ref_vocal/只想有你在身边 Yeah.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/pred_midi/只想有你在身边 Yeah.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/pred_vocal/只想有你在身边 Yeah.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/pred_cond_accomp/只想有你在身边 Yeah.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/pred_cond_song/只想有你在身边 Yeah.wav" type="audio/wav"></audio></td>
        </tr>
        </tbody>
    </table>

* Lyrics: 太阳不会放弃天空哪怕你不再属于我

  Pinyin: tai yang bu hui fang qi tian kong na pa ni bu zai shu yu wo

    <table style='width: 100%;'>
        <thead>
        <tr>
            <th></th>
            <th>GT Song</th>
            <th>GT Vocal</th>
            <th>GT MIDI</th>
            <th>Melody Prompts</th>
            <th>Accomp. Prompts</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <th scope="row">wav</th>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/gt_song/太阳不会放弃天空哪怕你不再属于我.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/gt_vocal/太阳不会放弃天空哪怕你不再属于我.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/gt_midi/太阳不会放弃天空哪怕你不再属于我.wav" type="audio/wav"></audio></td>
            <td style="text-align: center">This melody, within the tonal scale of D-flat major, carrying a high pitch and quick tempo for 10 seconds, emits sentimental energy.</td>
            <td style="text-align: center">This is a pop music piece. There is a female vocalist singing melodically in the lead. The melody is being played by the keyboard while the bass guitar is playing in the background. The rhythm is provided by a slow tempo acoustic drum beat. The atmosphere is emotional. This piece could be used in the soundtrack of a romance movie, especially during the scenes where a character is trying to break free. </td>
        </tr>
        </tbody>
    </table>

    <table style='width: 100%;'>
        <thead>
        <tr>
            <th></th>
            <th>Ref. Vocal</th>
            <th>Generated MIDI</th>
            <th>Generated Vocal</th>
            <th>Generated Accomp.</th>
            <th>Generated Song</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <th scope="row">wav</th>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/ref_vocal/太阳不会放弃天空哪怕你不再属于我.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/pred_midi/太阳不会放弃天空哪怕你不再属于我.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/pred_vocal/太阳不会放弃天空哪怕你不再属于我.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/pred_cond_accomp/太阳不会放弃天空哪怕你不再属于我.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/pred_cond_song/太阳不会放弃天空哪怕你不再属于我.wav" type="audio/wav"></audio></td>
        </tr>
        </tbody>
    </table>

* Lyrics: 宁可当作失败宁可重新再来

  Pinyin: ning ke dang zuo shi bai ning ke chong xin zai lai

    <table style='width: 100%;'>
        <thead>
        <tr>
            <th></th>
            <th>GT Song</th>
            <th>GT Vocal</th>
            <th>GT MIDI</th>
            <th>Melody Prompts</th>
            <th>Accomp. Prompts</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <th scope="row">wav</th>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/gt_song/宁可当作失败宁可重新再来.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/gt_vocal/宁可当作失败宁可重新再来.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/gt_midi/宁可当作失败宁可重新再来.wav" type="audio/wav"></audio></td>
            <td style="text-align: center">The song’s melody, composed in C sharp major, holds a high pitch and maintains a rapid pace, covering 5 seconds, filled with passionate and emotional qualities.</td>
            <td style="text-align: center">This music is an Electronica instrumental. The tempo is medium with a melodic pad and rhythmic acoustic guitar accompaniment. The music is soft, panned to the left channel of the stereo image. It is powerful, sentimental,emotional, passionate and emotional. </td>
        </tr>
        </tbody>
    </table>

    <table style='width: 100%;'>
        <thead>
        <tr>
            <th></th>
            <th>Ref. Vocal</th>
            <th>Generated MIDI</th>
            <th>Generated Vocal</th>
            <th>Generated Accomp.</th>
            <th>Generated Song</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <th scope="row">wav</th>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/ref_vocal/宁可当作失败宁可重新再来.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/pred_midi/宁可当作失败宁可重新再来.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/pred_vocal/宁可当作失败宁可重新再来.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/pred_cond_accomp/宁可当作失败宁可重新再来.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/pred_cond_song/宁可当作失败宁可重新再来.wav" type="audio/wav"></audio></td>
        </tr>
        </tbody>
    </table>

* Lyrics: 就请你告诉他你的名字我的名字

  Pinyin: jiu qing ni gao su ta ni de ming zi wo de ming zi

    <table style='width: 100%;'>
        <thead>
        <tr>
            <th></th>
            <th>GT Song</th>
            <th>GT Vocal</th>
            <th>GT MIDI</th>
            <th>Melody Prompts</th>
            <th>Accomp. Prompts</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <th scope="row">wav</th>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/gt_song/就请你告诉他你的名字我的名字.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/gt_vocal/就请你告诉他你的名字我的名字.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/gt_midi/就请你告诉他你的名字我的名字.wav" type="audio/wav"></audio></td>
            <td style="text-align: center">This part of the song, in A minor with a melody at a average pitch and average tempo lasting 10 seconds, carries a deep soulful feel.</td>
            <td style="text-align: center">The recording showcases a R&B song that consists of a passionate male vocal, alongside harmonizing background male vocals, singing over sustained strings melody, mellow piano chords, shimmering hi hats, punchy kick and snappy rimshots. It sounds emotional, passionate and soulful. </td>
        </tr>
        </tbody>
    </table>

    <table style='width: 100%;'>
        <thead>
        <tr>
            <th></th>
            <th>Ref. Vocal</th>
            <th>Generated MIDI</th>
            <th>Generated Vocal</th>
            <th>Generated Accomp.</th>
            <th>Generated Song</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <th scope="row">wav</th>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/ref_vocal/就请你告诉他你的名字我的名字.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/pred_midi/就请你告诉他你的名字我的名字.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/pred_vocal/就请你告诉他你的名字我的名字.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/pred_cond_accomp/就请你告诉他你的名字我的名字.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/pred_cond_song/就请你告诉他你的名字我的名字.wav" type="audio/wav"></audio></td>
        </tr>
        </tbody>
    </table>

* Lyrics: 直到生命最后一天

  Pinyin: zhi dao sheng ming zui hou yi tian

    <table style='width: 100%;'>
        <thead>
        <tr>
            <th></th>
            <th>GT Song</th>
            <th>GT Vocal</th>
            <th>GT MIDI</th>
            <th>Melody Prompts</th>
            <th>Accomp. Prompts</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <th scope="row">wav</th>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/gt_song/直到生命最后一天.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/gt_vocal/直到生命最后一天.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/gt_midi/直到生命最后一天.wav" type="audio/wav"></audio></td>
            <td style="text-align: center">The melody, flowing in E- major at a pitch of high and a tempo of fast, showcases lively tone.</td>
            <td style="text-align: center">This is an R&B music piece. There is a female vocalist singing melodically. The melody is being played by the keyboard while there is a bass guitar playing in the background. The rhythm is provided by a simple acoustic drum beat. The atmosphere is easygoing. This piece could be used in the soundtrack of a romantic movie, especially during the scenes where a character is reminiscing the good memories. </td>
        </tr>
        </tbody>
    </table>

    <table style='width: 100%;'>
        <thead>
        <tr>
            <th></th>
            <th>Ref. Vocal</th>
            <th>Generated MIDI</th>
            <th>Generated Vocal</th>
            <th>Generated Accomp.</th>
            <th>Generated Song</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <th scope="row">wav</th>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/ref_vocal/直到生命最后一天.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/pred_midi/直到生命最后一天.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/pred_vocal/直到生命最后一天.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/pred_cond_accomp/直到生命最后一天.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/pred_cond_song/直到生命最后一天.wav" type="audio/wav"></audio></td>
        </tr>
        </tbody>
    </table>

* Lyrics: 千万记得天涯有人在等待

  Pinyin: qian wan ji de tian ya you ren zai deng dai

    <table style='width: 100%;'>
        <thead>
        <tr>
            <th></th>
            <th>GT Song</th>
            <th>GT Vocal</th>
            <th>GT MIDI</th>
            <th>Melody Prompts</th>
            <th>Accomp. Prompts</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <th scope="row">wav</th>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/gt_song/千万记得天涯有人在等待.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/gt_vocal/千万记得天涯有人在等待.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/gt_midi/千万记得天涯有人在等待.wav" type="audio/wav"></audio></td>
            <td style="text-align: center">This segment’s melody in C sharp minor, with its relatively high pitch and swift tempo across 7 seconds, breathes a passionate essence.</td>
            <td style="text-align: center">This recording demonstrates a cover of a pop song and it consists of a passionate female vocal singing over sustained strings melody and mellow piano chords. It sounds emotional, passionate and the recording is noisy and in mono. </td>
        </tr>
        </tbody>
    </table>

    <table style='width: 100%;'>
        <thead>
        <tr>
            <th></th>
            <th>Ref. Vocal</th>
            <th>Generated MIDI</th>
            <th>Generated Vocal</th>
            <th>Generated Accomp.</th>
            <th>Generated Song</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <th scope="row">wav</th>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/ref_vocal/千万记得天涯有人在等待.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/pred_midi/千万记得天涯有人在等待.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/pred_vocal/千万记得天涯有人在等待.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/pred_cond_accomp/千万记得天涯有人在等待.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/pred_cond_song/千万记得天涯有人在等待.wav" type="audio/wav"></audio></td>
        </tr>
        </tbody>
    </table>

* Lyrics: 离别总在失意中度过

  Pinyin: li bie zong zai shi yi zhong du guo

    <table style='width: 100%;'>
        <thead>
        <tr>
            <th></th>
            <th>GT Song</th>
            <th>GT Vocal</th>
            <th>GT MIDI</th>
            <th>Melody Prompts</th>
            <th>Accomp. Prompts</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <th scope="row">wav</th>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/gt_song/离别总在失意中度过.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/gt_vocal/离别总在失意中度过.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/gt_midi/离别总在失意中度过.wav" type="audio/wav"></audio></td>
            <td style="text-align: center">This melody, set in B major with a average pitch and rapid tempo, lasts a medium period of time and carries a lively and happy aura.</td>
            <td style="text-align: center">This pop song features a male voice singing the main melody. Female voices sing backing vocals in harmony. This is accompanied by percussion playing a simple beat. The bass plays the root notes of the chords. Trumpets play a repetitive melody in the background. The mood of this song is happy. This song can be played in a romantic movie. </td>
        </tr>
        </tbody>
    </table>

    <table style='width: 100%;'>
        <thead>
        <tr>
            <th></th>
            <th>Ref. Vocal</th>
            <th>Generated MIDI</th>
            <th>Generated Vocal</th>
            <th>Generated Accomp.</th>
            <th>Generated Song</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <th scope="row">wav</th>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/ref_vocal/离别总在失意中度过.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/pred_midi/离别总在失意中度过.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/pred_vocal/离别总在失意中度过.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/pred_cond_accomp/离别总在失意中度过.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/pred_cond_song/离别总在失意中度过.wav" type="audio/wav"></audio></td>
        </tr>
        </tbody>
    </table>

* Lyrics: 我假装看不见我假装看不见因为害怕说抱歉

  Pinyin: wo jia zhuang kan bu jian wo jia zhuang kan bu jian yin wei hai pa shuo bao qian

    <table style='width: 100%;'>
        <thead>
        <tr>
            <th></th>
            <th>GT Song</th>
            <th>GT Vocal</th>
            <th>GT MIDI</th>
            <th>Melody Prompts</th>
            <th>Accomp. Prompts</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <th scope="row">wav</th>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/gt_song/我假装看不见我假装看不见因为害怕说抱歉.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/gt_vocal/我假装看不见我假装看不见因为害怕说抱歉.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/gt_midi/我假装看不见我假装看不见因为害怕说抱歉.wav" type="audio/wav"></audio></td>
            <td style="text-align: center">Set in the tonal realm of B flat major, this melody’s average pitch and average tempo through 7 seconds echo with happy essence.</td>
            <td style="text-align: center">This is a pop music piece. There is a male vocalist singing melodically in the lead. The main melody is being played by the keyboard while the bass guitar is playing in the background. The rhythm is provided by a slow tempo acoustic drum beat. The atmosphere is cheerful. This piece could be used in the soundtrack of a teenage drama TV series. </td>
        </tr>
        </tbody>
    </table>

    <table style='width: 100%;'>
        <thead>
        <tr>
            <th></th>
            <th>Ref. Vocal</th>
            <th>Generated MIDI</th>
            <th>Generated Vocal</th>
            <th>Generated Accomp.</th>
            <th>Generated Song</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <th scope="row">wav</th>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/ref_vocal/我假装看不见我假装看不见因为害怕说抱歉.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/pred_midi/我假装看不见我假装看不见因为害怕说抱歉.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/pred_vocal/我假装看不见我假装看不见因为害怕说抱歉.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/pred_cond_accomp/我假装看不见我假装看不见因为害怕说抱歉.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/pred_cond_song/我假装看不见我假装看不见因为害怕说抱歉.wav" type="audio/wav"></audio></td>
        </tr>
        </tbody>
    </table>

<!-- * Lyrics: 去思念爱情有点甜

  Pinyin: qu si nian ai qing you dian tian

    <table style='width: 100%;'>
        <thead>
        <tr>
            <th></th>
            <th>GT Song</th>
            <th>GT Vocal</th>
            <th>GT MIDI</th>
            <th>Melody Prompts</th>
            <th>Accomp. Prompts</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <th scope="row">wav</th>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/gt_song/去思念 爱情有点甜.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/gt_vocal/去思念 爱情有点甜.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/gt_midi/去思念 爱情有点甜.wav" type="audio/wav"></audio></td>
            <td style="text-align: center">The melody from this segment, cast in E major, holding a high pitch and medium tempo for a medium period of time, reverberates with passionate and emotional mood.</td>
            <td style="text-align: center">The recording showcases a passionate female vocal singing over punchy kick and snare hits, shimmering hi hats and groovy bass. It sounds addictive, passionate and emotional. </td>
        </tr>
        </tbody>
    </table>

    <table style='width: 100%;'>
        <thead>
        <tr>
            <th></th>
            <th>Ref. Vocal</th>
            <th>Generated MIDI</th>
            <th>Generated Vocal</th>
            <th>Generated Accomp.</th>
            <th>Generated Song</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <th scope="row">wav</th>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/ref_vocal/去思念 爱情有点甜.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/pred_midi/去思念 爱情有点甜.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/pred_vocal/去思念 爱情有点甜.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/pred_cond_accomp/去思念 爱情有点甜.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/pred_cond_song/去思念 爱情有点甜.wav" type="audio/wav"></audio></td>
        </tr>
        </tbody>
    </table> -->

* Lyrics: 我知道这样不是最好的决定

  Pinyin: wo zhi dao zhe yang bu shi zui hao de jue ding

    <table style='width: 100%;'>
        <thead>
        <tr>
            <th></th>
            <th>GT Song</th>
            <th>GT Vocal</th>
            <th>GT MIDI</th>
            <th>Melody Prompts</th>
            <th>Accomp. Prompts</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <th scope="row">wav</th>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/gt_song/我知道这样不是最好的决定.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/gt_vocal/我知道这样不是最好的决定.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/gt_midi/我知道这样不是最好的决定.wav" type="audio/wav"></audio></td>
            <td style="text-align: center">This musical segment in F sharp major, with a melody carrying a medium pitch and a quick tempo for 6 seconds, is steeped in easygoing essence.</td>
            <td style="text-align: center">The recorded music showcases a pop song that consists of a flat female vocal singing over electric guitar melody, groovy bass guitar, shimmering hi hats, punchy kick and snare hits. It sounds emotional and passionate. </td>
        </tr>
        </tbody>
    </table>

    <table style='width: 100%;'>
        <thead>
        <tr>
            <th></th>
            <th>Ref. Vocal</th>
            <th>Generated MIDI</th>
            <th>Generated Vocal</th>
            <th>Generated Accomp.</th>
            <th>Generated Song</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <th scope="row">wav</th>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/ref_vocal/我知道这样不是最好的决定.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/pred_midi/我知道这样不是最好的决定.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/pred_vocal/我知道这样不是最好的决定.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/pred_cond_accomp/我知道这样不是最好的决定.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midprompt_vocalref_to_song/pred_cond_song/我知道这样不是最好的决定.wav" type="audio/wav"></audio></td>
        </tr>
        </tbody>
    </table>


<h2 id="lyrics_melodyprompts_to_song">Lyrics + Melody Prompts -> Song</h2>

At this stage, we drop the reference vocals and accompaniment prompts, leaving the model only the lyrics and the melody prompts to build the melodies. Note that now the quality decreases since the model tends to randomly generate voices. 

* Lyrics: 宁可当作失败宁可重新再来

  Pinyin: ning ke dang zuo shi bai ning ke chong xin zai lai

    <table style='width: 100%;'>
        <thead>
        <tr>
            <th></th>
            <th>GT Song</th>
            <th>GT Vocal</th>
            <th>GT MIDI</th>
            <th>Melody Prompts</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <th scope="row">wav</th>
            <td><audio controls="" ><source src="resources/samples/lyrics_midiprompt_to_song/gt_song/宁可当作失败宁可重新再来.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midiprompt_to_song/gt_vocal/宁可当作失败宁可重新再来.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midiprompt_to_song/gt_midi/宁可当作失败宁可重新再来.wav" type="audio/wav"></audio></td>
            <td style="text-align: center">This segment, keyed in A-sharp minor, moves at a swift tempo with a pitch of relatively high, colored by passionate and emotional qualities.</td>
        </tr>
        </tbody>
    </table>

    <table style='width: 100%;'>
        <thead>
        <tr>
            <th></th>
            <th>Generated MIDI</th>
            <th>Generated Vocal</th>
            <th>Generated Accomp.</th>
            <th>Generated Song</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <th scope="row">wav</th>
            <td><audio controls="" ><source src="resources/samples/lyrics_midiprompt_to_song/pred_midi/宁可当作失败宁可重新再来.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midiprompt_to_song/pred_vocal/宁可当作失败宁可重新再来.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midiprompt_to_song/pred_cond_accomp/宁可当作失败宁可重新再来.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midiprompt_to_song/pred_cond_song/宁可当作失败宁可重新再来.wav" type="audio/wav"></audio></td>
        </tr>
        </tbody>
    </table>

* Lyrics: 让疯狂慢慢从爱情离开

  Pinyin: rang feng kuang man man cong ai qing li kai

    <table style='width: 100%;'>
        <thead>
        <tr>
            <th></th>
            <th>GT Song</th>
            <th>GT Vocal</th>
            <th>GT MIDI</th>
            <th>Melody Prompts</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <th scope="row">wav</th>
            <td><audio controls="" ><source src="resources/samples/lyrics_midiprompt_to_song/gt_song/让疯狂慢慢从爱情离开.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midiprompt_to_song/gt_vocal/让疯狂慢慢从爱情离开.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midiprompt_to_song/gt_midi/让疯狂慢慢从爱情离开.wav" type="audio/wav"></audio></td>
            <td style="text-align: center">This piece in D-flat major resonates with a medium pitch at a gentle tempo for a medium period of time, filled with religious emotions.</td>
        </tr>
        </tbody>
    </table>

    <table style='width: 100%;'>
        <thead>
        <tr>
            <th></th>
            <th>Generated MIDI</th>
            <th>Generated Vocal</th>
            <th>Generated Accomp.</th>
            <th>Generated Song</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <th scope="row">wav</th>
            <td><audio controls="" ><source src="resources/samples/lyrics_midiprompt_to_song/pred_midi/让疯狂慢慢从爱情离开.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midiprompt_to_song/pred_vocal/让疯狂慢慢从爱情离开.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midiprompt_to_song/pred_cond_accomp/让疯狂慢慢从爱情离开.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midiprompt_to_song/pred_cond_song/让疯狂慢慢从爱情离开.wav" type="audio/wav"></audio></td>
        </tr>
        </tbody>
    </table>

* Lyrics: 爱你的路

  Pinyin: ai ni de lu

    <table style='width: 100%;'>
        <thead>
        <tr>
            <th></th>
            <th>GT Song</th>
            <th>GT Vocal</th>
            <th>GT MIDI</th>
            <th>Melody Prompts</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <th scope="row">wav</th>
            <td><audio controls="" ><source src="resources/samples/lyrics_midiprompt_to_song/gt_song/爱你的路.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midiprompt_to_song/gt_vocal/爱你的路.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midiprompt_to_song/gt_midi/爱你的路.wav" type="audio/wav"></audio></td>
            <td style="text-align: center">In G major, the melody rises with a relatively high pitch and flows at a rapid tempo for a short period, oozing passionate and emotional mood.</td>
        </tr>
        </tbody>
    </table>

    <table style='width: 100%;'>
        <thead>
        <tr>
            <th></th>
            <th>Generated MIDI</th>
            <th>Generated Vocal</th>
            <th>Generated Accomp.</th>
            <th>Generated Song</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <th scope="row">wav</th>
            <td><audio controls="" ><source src="resources/samples/lyrics_midiprompt_to_song/pred_midi/爱你的路.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midiprompt_to_song/pred_vocal/爱你的路.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midiprompt_to_song/pred_cond_accomp/爱你的路.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midiprompt_to_song/pred_cond_song/爱你的路.wav" type="audio/wav"></audio></td>
        </tr>
        </tbody>
    </table>

* Lyrics: 撑到现在早没什么用

  Pinyin: cheng dao xian zai zao mei shen me yong

    <table style='width: 100%;'>
        <thead>
        <tr>
            <th></th>
            <th>GT Song</th>
            <th>GT Vocal</th>
            <th>GT MIDI</th>
            <th>Melody Prompts</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <th scope="row">wav</th>
            <td><audio controls="" ><source src="resources/samples/lyrics_midiprompt_to_song/gt_song/撑到现在早没什么用.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midiprompt_to_song/gt_vocal/撑到现在早没什么用.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midiprompt_to_song/gt_midi/撑到现在早没什么用.wav" type="audio/wav"></audio></td>
            <td style="text-align: center">The melody in this part of the song, set in G minor with a average pitch at a quick tempo for a short period of time, envelops the listener with easygoing atmosphere.</td>
        </tr>
        </tbody>
    </table>

    <table style='width: 100%;'>
        <thead>
        <tr>
            <th></th>
            <th>Generated MIDI</th>
            <th>Generated Vocal</th>
            <th>Generated Accomp.</th>
            <th>Generated Song</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <th scope="row">wav</th>
            <td><audio controls="" ><source src="resources/samples/lyrics_midiprompt_to_song/pred_midi/撑到现在早没什么用.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midiprompt_to_song/pred_vocal/撑到现在早没什么用.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midiprompt_to_song/pred_cond_accomp/撑到现在早没什么用.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_midiprompt_to_song/pred_cond_song/撑到现在早没什么用.wav" type="audio/wav"></audio></td>
        </tr>
        </tbody>
    </table>

<h2 id="lyrics_to_song">Lyrics -> Song</h2>

Finally, we explore the scenario that only the lyrics are available. All the left attributes are generated unconditionally and randomly, resulting in a intangible performance.


* Lyrics: 铸成一个死结

  Pinyin: zhu cheng yi ge si jie

    <table style='width: 100%;'>
        <thead>
        <tr>
            <th></th>
            <th>GT Song</th>
            <th>GT Vocal</th>
            <th>Generated Vocal</th>
            <th>Generated Song</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <th scope="row">wav</th>
            <td><audio controls="" ><source src="resources/samples/lyrics_to_song/gt_song/铸成一个死结.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_to_song/gt_vocal/铸成一个死结.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_to_song/pred_vocal/铸成一个死结.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_to_song/pred_uncond_song/铸成一个死结.wav" type="audio/wav"></audio></td>
        </tr>
        </tbody>
    </table>

* Lyrics: 自己定的规则却不肯复刻无可奈何的感觉又无从改善我累了

  Pinyin: zi ji ding de gui ze que bu ken fu ke wu ke nai he de gan jue you wu cong gai shan wo lei le

    <table style='width: 100%;'>
        <thead>
        <tr>
            <th></th>
            <th>GT Song</th>
            <th>GT Vocal</th>
            <th>Generated Vocal</th>
            <th>Generated Song</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <th scope="row">wav</th>
            <td><audio controls="" ><source src="resources/samples/lyrics_to_song/gt_song/自己定的规则却不肯复刻无可奈何的感觉又无从改善我累了.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_to_song/gt_vocal/自己定的规则却不肯复刻无可奈何的感觉又无从改善我累了.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_to_song/pred_vocal/自己定的规则却不肯复刻无可奈何的感觉又无从改善我累了.wav" type="audio/wav"></audio></td>
            <td><audio controls="" ><source src="resources/samples/lyrics_to_song/pred_uncond_song/自己定的规则却不肯复刻无可奈何的感觉又无从改善我累了.wav" type="audio/wav"></audio></td>
        </tr>
        </tbody>
    </table>

