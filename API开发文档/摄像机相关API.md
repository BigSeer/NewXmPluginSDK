FastVideo ʹ��˵��
ApiLevel 62

Ŀǰ��Ҫʹ��SmartHome_camera_debug.apk ���е���

һ����Ƶ����
	�ӿ� XmPluginHostApi
	����һ������ʵʱ������ͼ ���ز�����ͼ�Ľӿ�
 
     /**
     * 
     * ����һ��������Ƶ���Ĳ�����ͼ
     *
     * @param context
     * @param original ������
     * @param useHard  �Ƿ�����ʹ��Ӳ����
     * @param type     ��Ƶ���������� 1==h264 2==h265
     * @return
     * @see com.xiaomi.smarthome.camera.VideoFrame
     */
	public abstract XmVideoViewGl createVideoView(Context context, FrameLayout original, boolean useHard, int type);
	
	ʹ�����ӣ�		
    FrameLayout.LayoutParams lp = new FrameLayout.LayoutParams(FrameLayout.LayoutParams.MATCH_PARENT,FrameLayout.LayoutParams.MATCH_PARENT);
    FrameLayout layout = new FrameLayout(activity());
    mVideoView = XmPluginHostApi.instance().createVideoView(activity(), layout, true, VideoFrame.VIDEO_H264);
	layout������Ҫ��ʾ��Ƶ����ͼ��������New��Ҳ��������XML�����еģ�
 
	����һ������Mp4����ͼ ���ز�����ͼ�Ľӿ�
    /**
     *
     * ����һ���������ű���Mp4����ͼ ���ز�����ͼ�Ľӿ�
     *	Mp4���ŵĿ��� XmVideoViewGl getMp4Player() �����᷵��һ��Mp4���ƵĽӿ�
     * @param context
     * @param original ������
     * @param useHard  true MediaPlayer����mp4��false ʹ��ffmpeg ����mp4
     * @return
     */
   ��public abstract XmVideoViewGl createMp4View(Context context, FrameLayout original, boolean useHard);

    ʹ�����ӣ�
	FrameLayout.LayoutParams lp = new FrameLayout.LayoutParams(FrameLayout.LayoutParams.MATCH_PARENT, FrameLayout.LayoutParams.MATCH_PARENT);
    FrameLayout layout = new FrameLayout(activity());
	XmVideoViewGl xmVideoViewGl = XmPluginHostApi.instance().createMp4View(activity(), layout, true);    
	XmMp4Player xmMp4Player = xmVideoViewGl.getMp4Player();
	xmVideoViewGl ����������Ƶ������ع���
	xmMp4Player ��������Mp4��ع���
	layout ����Ҫ��ʾ����ͼ ��Ҫ��FrameLayout
	����ֻ�����֧��Mp4����Ƶ���Ĳ��ţ�useHard���true  �ֻ�����֧��Mp4����Ƶ���Ĳ���(�Ͱ汾�ֻ���֧��h265)��useHard���false
	
	
����������� 
	����豸�޷����л������SDK�ṩ�����Ļ����������,���ṩVideoFrame ʱ��ù��캯����Ҫ���ݲ����Ҫ�Ļ�������
	 
	//0��������� 1 ���������ʱ��ˮӡ 2���������ʱ��ˮӡ
    public static final int DISTORT_NONE = 0;
    public static final int DISTORT_ALL = 1;
    public static final int DISTORT_PART = 2;
	     /**
     * ������Ƶ��
     *
     * @param data        ����
     * @param frameNumber ֡���
     * @param frameSize   ��С
     * @param width       ��
     * @param height      ��
     * @param timestamp   ʱ���
     * @param videoType   ��Ƶ������1:h264 2:h265
     * @param isIFrame    �Ƿ���I֡
     * @param distrot     �����״̬
     * @param isReal      �Ƿ���ʵʱ��
     */
    public VideoFrame(byte[] data,
                      long frameNumber, int frameSize,
                      int width, int height,
                      long timestamp, int videoType, boolean isIFrame, int distrot, boolean isReal) {
					  }

   /**
     * �����������з�Χ����Ҫ���� �����ھ�����ʵʱ��ʱ�����ʾ���⣩
     *
     * @param x ��������Ͻ�X��
     * @param y ��������Ͻ�Y��
     */
    public void setDistort(float x, float y) {
        mDistortX = x;
        mDistortY = y;
    }					  


����Mp4�ĺϳ�
	1.���� XmPluginHostApi.createMp4Record() �᷵��һ��XmMp4Record �ӿ���������Mp4�ĺϳɸ����ӿ�

	2.XmMp4Record  �ϳ�ʱ����Ƶ��֧�֣�h264/h265�� ��Ƶ֧�֣�aac������豸���ݹ�������������Ƶ��ʽ��Ҫ����Լ�ת����aac��ʼ��ʱ����Ҫ�ṩ mp4�ϳɵĲ���
    /**
     * 
     * @param fileName �ϳ�Mp4���ļ�ȫ·��
     * @param videoType ��Ƶ������(h264-h265) @see H264Decoder
     * @param width ��Ƶ�����
     * @param height ��Ƶ���߶�
     * @param audioSample ��Ƶ������
     */
	public void startRecord(String fileName, int videoType, int width, int height, int audioSample);
     /**
     * 
     * @param data д�����Ƶ������(һ֡)
     * @param length (���ݳ���)
     * @param isIFrame ���Ƿ���I ֡��
     * @param time ʱ���
     */
	public  void writeVideoData(byte[] data, int length, boolean isIFrame, int time);
  
	/**
     * д����Ƶ����
     * @param data ����
     * @param length ���ݳ���
     */
	public  void writeAAcData(byte[] data, int length);
  
	/**
     * ����¼��
     * @param listener ����ص��Ƿ�¼�Ƴɹ�
     */
	public void stopRecord(final IRecordListener listener);

�ġ�Mp4�Ĳ���
	ͨ������ XmPluginHostApi.instance().createMp4View(Context context, FrameLayout original, boolean useHard) ����һ��Mp4�Ĳ�����ͼ�ӿ� XmVideoViewGl
	Ȼ��ͨ������XmVideoViewGl.getMp4Player() ����XmMp4Player ��������Mp4���ŵĸ����ӿ�

	SDK�ṩ������Mp4����ģʽ(FFmpeg���š�MediaPlayer����)
	1.MediaPlayer ���ţ�
	
	ʹ��VideoGlSurfaceView ������Ⱦ,��ʼ����ʱ����Ҫʹ�� VideoPlayerRender���н������
	
	2.FFmpeg����: �ֻ�����֧��Mp4����Ƶ���Ĳ���(�Ͱ汾�ֻ���֧��h265)
	ʹ��VideoGlSurfaceView ������Ⱦ,��ʼ����ʱ����Ҫʹ�� VideoPlayerFFmpeg���н������
